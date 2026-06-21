# 呼吸困難 評価ツール（RDOS / IC-RDOS / MV-RDOS）

自己申告ができない患者の呼吸困難（dyspnoea）を、観察スケールから推定するためのWebアプリです。
RDOS・IC-RDOS・MV-RDOS の3スケールをタブで切り替えて計算できます。

- **RDOS**（8項目, 0〜16点）… 緩和ケア〜一般病棟まで、自己申告できない患者全般（非挿管を含む）
- **IC-RDOS**（5項目, 加重式, 閾値 2.4）… ICU患者向け。酸素投与の有無を含む
- **MV-RDOS**（5項目, 加重式, 閾値 2.6）… 挿管・人工呼吸患者向け。呼吸数を含む

依存ファイルなしの単一HTML（フォントのみGoogle FontsをCDN参照）。`index.html` を開くだけで動作します。

---

## GitHub Pages で公開する手順

1. GitHub で新しいリポジトリを作成する（例: `dyspnea-rdos`）。Public を推奨。
2. このフォルダの `index.html`（必要なら `README.md` も）をリポジトリに追加して push、または
   GitHub 画面の **Add file → Upload files** でアップロードして commit。
3. リポジトリの **Settings → Pages** を開く。
4. **Build and deployment → Source** を **Deploy from a branch** にし、
   **Branch** を `main` ／ フォルダを `/ (root)` に設定して **Save**。
5. 数十秒〜数分後、`https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます。

> 補足: `index.html` をリポジトリ直下に置くと、そのまま `/` で表示されます。
> 病院ネットワークなど外部CDNが遮断される環境では、Google Fonts が読み込めず
> 既定フォントで表示されますが、計算機能はそのまま動作します。

### コマンド例（任意）

```bash
git init
git add index.html README.md
git commit -m "Add dyspnoea RDOS calculator"
git branch -M main
git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
git push -u origin main
# その後、Settings → Pages で main / root を有効化
```

## ローカルで使う

`index.html` をダブルクリックしてブラウザで開くだけで使えます。

---

## 計算式

- **RDOS** = 8項目（心拍数・呼吸数・落ち着きのなさ・頸部筋使用・奇異性呼吸・呼気終末のうめき・鼻翼呼吸・恐怖表情）を各0〜2点で合計（0〜16）。
  カットオフ: 0–2 なし〜ごく軽度 / 3 軽度 / 4–6 中等度 / ≥7 重度。
- **IC-RDOS** = 3.3 +（HR/65）+ 頸部筋 + 奇異性呼吸 + 恐怖表情 + 酸素投与。各項目 あり+1 / なし−1、酸素は ±0.7。閾値 2.4。
- **MV-RDOS** = 3.3 +（HR/65）+（RR/50）+ 頸部筋 + 奇異性呼吸 + 恐怖表情。各項目 あり+1 / なし−1。閾値 2.6（>4前後で特異度が高い）。

## 注意

本ツールは臨床判断の補助を目的とした計算機であり、診断や治療方針の決定に代わるものではありません。
意思疎通が可能な患者では、まずVAS／NRSによる自己申告を優先してください。
最終的な判断は担当医が患者の全体像を踏まえて行ってください。

## 参考文献

- Decavèle M, et al. Respiratory distress observation scales to predict weaning outcome. *Critical Care* 2022;26:162.
- Demoule A, et al. Dyspnoea in acutely ill mechanically ventilated adult patients: an ERS/ESICM statement. *Eur Respir J* 2024;63:2300347.
- Campbell ML, et al. A Respiratory Distress Observation Scale for patients unable to self-report dyspnea. *J Palliat Med* 2010;13:285–290.
- Campbell ML, Kero KK, Templin TN. Mild, moderate, and severe intensity cut-points for the RDOS. *Heart Lung* 2017;46:14–17.
- Persichini R, et al. Diagnostic accuracy of respiratory distress observation scales (IC-RDOS). *Anesthesiology* 2015;123:830–837.
- Decavèle M, et al. The MV-RDOS as a surrogate of self-reported dyspnoea in intubated patients. *Eur Respir J* 2018;52:1800598.

オンライン計算機: https://dos-calc.pvsc.fr
