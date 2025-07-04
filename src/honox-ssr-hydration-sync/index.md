---
marp: true
theme: suntory-n-water
paginate: true
image: https://suntory-n-water.github.io/sui-marp-template/honox-ssr-hydration-sync/index.png
title: HonoXにおけるSSRとクライアントサイドHydrationの同期問題
description: HonoXでSSRとクライアントサイドHydrationの同期問題を解決する方法
keywords: HonoX, SSR, Hydration, React, JavaScript
---

<!-- _class: lead -->

# HonoXにおける
# SSRとクライアントサイド
# Hydrationの同期問題

---

<!-- _class: invert -->

## 問題の概要

HonoXでSSRされたコンポーネントの表示が、クライアントサイドのHydration時に初期状態に戻ってしまう問題

**具体的な現象**
- URLパラメータ `/?sort=random` でアクセス
- コンテンツは正しくランダム順で表示
- しかし、ドロップダウンは「新着順」のままになる

---

## 今回のケース

**金髪ヒロイン.com** のキャラクター一覧ページでの事例

URLパラメータによるソート機能の実装で発生した問題

---

## サーバーサイドの実装

サーバーサイドでは正常に動作

:::_ {.text-sm}

```tsx
export default createRoute(async (c) => {
  const sortQuery = c.req.query('sort');
  const currentSort = sortQuery || 'newest';
  
  return c.render(
    <SortSelector 
      currentSort={currentSort} 
      options={sortOptions} 
    />
  );
});
```
:::

---

## クライアントサイドの実装

クライアントサイドで問題が発生

:::_ {.text-sm}

```tsx
export function SortSelector({ currentSort, options }) {
  return (
    <select value={currentSort} onChange={handleChange}>
      {options.map(option => (
        <option key={option.key} value={option.key}>
          {option.label}
        </option>
      ))}
    </select>
  );
}
```

:::

---

## 原因の調査プロセス

サーバーサイドとクライアントサイドを段階的に確認した結果、コンポーネントは正しいプロパティを受け取っているが、DOM要素に反映されないことが判明

- **サーバーサイド**: URLパラメータ解析、プロパティ受け渡しは正常
- **クライアントサイド**: コンポーネント実装に明らかな問題なし
- **デバッグログ**: プロパティは正しく受け取られている

---

## 根本原因の分析

Hydration時のReact仮想DOM同期でvalue属性の再適用が失敗し、初期選択状態に戻ってしまう

**HonoXフロー**: SSRでHTML生成 → ブラウザ送信 → JavaScriptでHydration

**問題メカニズム**: SSR時は`value="random"`で正しいHTMLが生成されるが、Hydration時にReactが仮想DOMと同期しようとしてvalue属性の再適用に失敗し、最初の`<option>`が選択される

---

## 解決策の実装

useEffectを使った明示的な状態同期

---

## 解決策のコード

```tsx
import { useEffect } from 'hono/jsx/dom';

export function SortSelector({ currentSort, options }) {
  useEffect(() => {
    const select = document.querySelector('select[name="sort"]');
    if (select && select instanceof HTMLSelectElement) {
      select.value = currentSort;
    }
  }, [currentSort]);

  return (
    <form method='get' action=''>
      <select
        name='sort'
        defaultValue={currentSort}  // valueからdefaultValueに変更
        onChange={handleChange}
      >
        {options.map(option => (
          <option key={option.key} value={option.key}>
            {option.label}
          </option>
        ))}
      </select>
    </form>
  );
}
```

---

## 解決策のポイント

`defaultValue`と`useEffect`を組み合わせてSSRとクライアント状態を明示的に同期

**アプローチ**:
- **`defaultValue`**: 初期HTML生成時の値設定、状態管理競合回避  
- **`useEffect`**: DOMマウント後の確実な値同期、プロパティ変更時再実行

**結果**: SSRの高速初期表示 + クライアントの正確な状態表示

---

## 試行錯誤したその他のアプローチ

解決策に至るまでに試した3つのアプローチ

---

## ❌ defaultValueのみの使用

```tsx
<select defaultValue={currentSort}>
```

**問題**: 初期表示は正しいが、プロパティ変更時に追従しない

---

## ❌ key属性によるコンポーネント再マウント

```tsx
<select key={currentSort} value={currentSort}>
```

**問題**: パフォーマンスへの影響、UXの問題（アニメーション中断）

---

## ❌ ref属性の使用

```tsx
<select ref={selectRef} value={currentSort}>
```

**問題**: HonoXのJSX実装でrefプロパティが未サポート

---

## 重要な学び

SSRフレームワークではサーバーとクライアントの状態を明示的に同期させることが重要

**状態管理の鉄則**:
- サーバーとクライアントの状態を常に意識
- 明示的同期処理が必要な場合あり
- `useEffect`でDOMレベル制御を活用

**デバッグアプローチ**: プロパティ受け渡し確認 → DOM実際状態チェック → SSR/Hydration境界を意識した原因分析

---

## まとめ

**問題**: HonoXでSSRされたコンポーネントがHydration時に初期状態に戻る

**解決策**: 
- `defaultValue` による初期HTML生成
- `useEffect` による明示的な状態同期

**教訓**: 
SSRフレームワークでは、サーバーとクライアントの状態を明示的に同期させる必要がある場合がある

この知識は、HonoXに限らず他のSSRフレームワークでも応用できる重要な概念です。

---

<!-- _class: invert -->

## 参考情報

**実際のプロジェクト**: [金髪ヒロイン.com](https://kinpatsu-heroine.com/)