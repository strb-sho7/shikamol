<img src="apple-touch-icon.png" width="72" align="right" alt="">

# ShikaMol

ブラウザで動く分子ビューアです。

[English](README.md) | **日本語**

ブラウザだけで動く分子ビューアです。PDB ID かファイルを読み込むだけで、構造の表示、電子密度・クライオ電顕マップの重ね合わせ、残基どうしの相互作用の解析、論文用の高解像度画像の書き出しまでを一つの画面で行えます。インストールは要りません。パソコン・iPad・スマートフォンのブラウザで動きます。

**▶ 使ってみる：https://strb-sho7.github.io/shikamol/**

---

## 使い方

1. 上のアドレスを開きます。
2. 左の「構造」タブで、PDB ID（例 `7DA1`。`pdb_00007da1` のような 12 文字の形でも可）を入力して「読込」を押します。手元の `.pdb` / `.cif` ファイルを読み込むこともできます（ドラッグ＆ドロップ可）。
3. 分子ウィンドウで残基をクリック（タブレットではタップ）すると、その残基にズームし、周囲 5 Å 以内の相互作用が一覧と点線で表示されます。背景をクリックすると解除されます。

### アドレスで構造を指定する

アドレスの末尾に `?pdb=` を付けると、開いたときにその構造を読み込みます。授業で「今日の構造」を配るときに便利です。

```
https://strb-sho7.github.io/shikamol/?pdb=7DA1
```

## 主な機能

**表示**
- Chain ごとの色分け、表示形式（カートゥーン・スティック・表面など）の切り替え
- 表面の色分け：疎水性、保存度、APBS の静電ポテンシャル（`.dx` を読み込み）
- 配列の帯：画面下に配列を表示し、クリックやドラッグで残基を選択
- 選択の保存：選んだ残基に名前・色・表示形式を付けて残し、表示を切り替え
- 範囲選択：分子ウィンドウ上をドラッグして、四角で囲んだ残基を選択
- 周りを薄くする表示：注目している残基から一定の距離より外側を薄くする
- 対称分子：結晶構造の対称分子を表示し、選んだものを Chain として加えて解析
- 生物学的集合体：RCSB に登録された集合体の座標を読み込み
- 複数の構造の読み込みと重ね合わせ

**電子密度・マップ**
- X 線結晶構造：PDBe の密度サーバーから 2mFo-DFc / mFo-DFc マップを取得し、クリックした残基の周りに球状の範囲で表示
- クライオ電顕構造：EMDB のマップを、登録された推奨の等高線レベルで表示
- 手元のマップファイル（`.ccp4` / `.map` / `.mrc` など）の読み込み

**解析**
- クリックした残基の相互作用の一覧：水素結合、塩橋、疎水性相互作用、π スタッキング、カチオン–π、金属配位、ハロゲン結合、水を介した水素結合
  - 種類ごとの表示・非表示、主鎖どうしの相互作用の表示・非表示
  - 距離の判定基準は「解析」タブで変更可能（水素結合の初期値はドナー–アクセプター間 3.5 Å、硫黄が関わる場合は +0.6 Å）
- Chain 間の界面の解析：界面の残基の組、埋没表面積（BSA）、界面面積
- 保存度（ConSurf 風）：多重配列アラインメント（MSA）から計算するか、ConSurf の結果ファイルを読み込んで色分け

**出力**
- 論文用の PNG 書き出し：幅（mm / inch / px）と解像度（dpi）を指定して、600 dpi 以上でも書き出し可能
- 相互作用の一覧のコピー（表計算ソフトに貼り付け可能）
- セッションの保存・読み込み：表示や解析の状態を `.json` ファイルに保存
- 日本語 / English の切り替え

## データの扱い

- 手元から読み込んだファイル（構造・マップ・MSA など）は、すべてブラウザの中だけで処理されます。どこにも送信されません。未発表の構造も安心して使えます。
- PDB ID から読み込むときは、RCSB PDB・PDBe・EMDB の公開データを取得します。

## iPad・タブレットで使うとき

- タップで残基の選択、背景のタップで解除、1 本指のドラッグで回転、2 本指でズームと移動ができます。
- 配列の帯は、長押ししてからなぞると範囲を選べます。
- ダウンロードしたファイルの名前が `1abc.pdb.txt` のようになっていても、そのまま読み込めます。
- Safari の共有ボタン →「ホーム画面に追加」で、アプリのように起動できます。

## 動作環境

Chrome、Edge、Safari、Firefox の最新版。WebGL が使えるブラウザが必要です。

index.html だけをダウンロードして開いた場合は、同じフォルダに ngl.js がないため、NGL をインターネット（unpkg）から読み込みます。

## 使っているライブラリ・データ・計算方法

**ライブラリ**
- NGL Viewer 2.3.1（MIT ライセンス）。ShikaMol と同じ場所に置いた `ngl.js` を読み込みます（npm パッケージ ngl 2.3.1 の `dist/ngl.js` を改変せずに同梱）。`ngl.js` に含まれる three.js・Mol\*・chroma.js・sprintf-js・JS-Signals を含め、ライセンス文は [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt) にまとめています。
  - Rose AS, Hildebrand PW. NGL Viewer: a web application for molecular visualization. *Nucleic Acids Res.* 2015;43:W576–W579. doi:[10.1093/nar/gkv402](https://doi.org/10.1093/nar/gkv402)
  - Rose AS, et al. NGL viewer: web-based molecular graphics for large complexes. *Bioinformatics.* 2018;34:3755–3758. doi:[10.1093/bioinformatics/bty419](https://doi.org/10.1093/bioinformatics/bty419)

**データ**
- RCSB PDB（座標、エントリー情報、生物学的集合体）
- PDBe の密度サーバー（X 線結晶構造の電子密度）
- EMDB（クライオ電顕マップと推奨の等高線レベル）

**計算方法**
- 相互作用の種類と判定基準は、PLIP と Mol* を参考にしています。
  - Salentin S, et al. PLIP: fully automated protein–ligand interaction profiler. *Nucleic Acids Res.* 2015;43:W443–W447. doi:[10.1093/nar/gkv315](https://doi.org/10.1093/nar/gkv315)
  - Sehnal D, et al. Mol* Viewer: modern web app for 3D visualization and analysis of large biomolecular structures. *Nucleic Acids Res.* 2021;49:W431–W437. doi:[10.1093/nar/gkab314](https://doi.org/10.1093/nar/gkab314)
- 界面面積は PISA と同じ定義（埋没表面積の合計の 1/2）です。
  - Krissinel E, Henrick K. Inference of macromolecular assemblies from crystalline state. *J. Mol. Biol.* 2007;372:774–797. doi:[10.1016/j.jmb.2007.05.022](https://doi.org/10.1016/j.jmb.2007.05.022)
- 保存度は Jensen–Shannon divergence で計算し、ConSurf と同じ 9 段階に分けて色分けしています。
  - Capra JA, Singh M. Predicting functionally important residues from sequence conservation. *Bioinformatics.* 2007;23:1875–1882. doi:[10.1093/bioinformatics/btm270](https://doi.org/10.1093/bioinformatics/btm270)

## 作者

伊藤 翔（奈良先端科学技術大学院大学）

不具合の報告や要望は、このリポジトリの「Issues」からお願いします。
