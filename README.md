# InfraManage

AI-assisted road-damage reporting and maintenance prioritisation for townships and councils.

**Domain:** Smart township and municipal infrastructure maintenance (initial focus: road damage)

---

## Problem Statement

Maintenance teams receive damage reports as scattered photos and messages, with no consistent way to tell what the damage is, whether it was already reported, or how urgent it is. Road users, especially motorcyclists, bear the risk and repair costs.

AI can detect the damage type from photos, group duplicate reports into one incident using image similarity and location, and recommend an explainable priority, with officers keeping the final decision.

## What the System Does

1. A resident submits a report with a photo, GPS location and timestamp.
2. AI detects the damage type (pothole, longitudinal crack, transverse crack, alligator crack).
3. The system groups likely duplicate reports into one incident, keeping every photo.
4. A risk priority score is calculated and shown with its reasons.
5. An officer reviews the result on a map dashboard and can confirm, override or split incidents.
6. Repair status is tracked until the damage is fixed.

## Evidence of the Problem

- **Evidence 1:** JKR patched 168,003 potholes in 2020 along 14,385 km of federal roads, and over 55,800 potholes were reported in 2024.
  Sources: [FMT (2021)](https://www.freemalaysiatoday.com/category/nation/2021/01/17/jkr-opens-up-on-the-thousands-of-potholes-on-roads), [RinggitPlus](https://ringgitplus.com/en/blog/personal-finance-news/a-rm1-8bil-pothole-in-govt-finances-the-high-cost-of-malaysias-underfunded-roads.html)
- **Evidence 2:** Reporting is fragmented. JKR listed 11 complaint channels, and the public accused it of responding fast only when a minister was affected.
  Sources: [The Vibes](https://www.thevibes.com/articles/news/11597/jkr-gives-11-ways-to-channel-complaints-after-kj-pothole-uproar), [The Rakyat Post](https://www.therakyatpost.com/living/2020/12/29/jkr-lists-11-official-ways-to-complain-about-potholes-bad-roads-after-malaysians-complain-of-double-standards/)
- **Evidence 3:** Police statistics cited by a MIROS board member recorded 55 deaths from pothole-related crashes in 2018, plus 16 serious and 40 minor injuries. This was about 0.88% of national road fatalities, so potholes are a small but preventable, maintenance-related share. The data does not say whether crashes were on federal or local roads.
  Source: [The Vibes (Shahrim Tamrin)](https://www.thevibes.com/articles/opinion/14662/fatal-pothole-accidents-on-the-rise-shahrim-tamrim)
- **Evidence 4:** In January 2021 a senior citizen on a motorcycle died after hitting potholes on Jalan Tengah near Mid Valley, Kuala Lumpur.
  Source: [The Vibes (Shahrim Tamrin)](https://www.thevibes.com/articles/opinion/14662/fatal-pothole-accidents-on-the-rise-shahrim-tamrim)
- **Evidence 5:** Duplicate reports cost municipalities money, and authorities often still check for duplicate or fake reports and rate severity by hand, causing delays and a growing backlog.
  Sources: [Zhang & Wang (2015)](https://xreiss.efri.uniri.hr/article.php?id=44937), [Salcedo et al. (2022)](https://doi.org/10.3390/jsan11010015)

## Initial Related Work

| # | Study / solution | Source | Key limitation |
|---|---|---|---|
| 1 | **RDD2022 (Arya et al.):** 47,420 images from six countries, with over 55,000 annotated damages in four types | [arXiv](https://arxiv.org/abs/2209.08538) | Malaysia is not among the six countries; detection only |
| 2 | **Sharma et al., road monitoring pilot:** YOLOv8 F1 of 0.45 during fine-tuning; 65% of images rated satisfactory or better by professionals | [TRID](https://trid.trb.org/View/2715341) | Real-world detection is far below benchmark scores; confuses similar-looking objects |
| 3 | **Salcedo et al. (2022):** road segmentation, YOLOv5 detection (single cracks, crocodile cracks, potholes), image-based duplicate matching (SIFT and FLANN, about 85% precision), location clustering with a weighted-sum priority | [J. Sens. Actuator Netw.](https://doi.org/10.3390/jsan11010015) | Duplicates use images only (no GPS or time); priority counts damage types only; clustering tested on synthetic data; traffic density left as future work |
| 4 | **Aberdeenshire Council, risk-based defect scoring:** scores a pothole by position on the road, size and speed limit | [Aberdeenshire Council](https://www.aberdeenshire.gov.uk/media/28117/roadinspectionsummary.pdf) | Manual inspector process; no automatic photo analysis |
| 5 | **MYJalan app:** GPS tagging, photo upload, status tracking | [Borneo Post](https://www.theborneopost.com/?p=1339583) | No automatic damage classification or risk scoring described |

## Engineering Gap / Limitation

Earlier work already combines parts of this pipeline (Salcedo et al.), so the gap is in how well it fits a real township workflow:

1. Duplicate matching there uses images only, while InfraManage also uses GPS and timestamps.
2. Priority there counts damage types and ignores road type and traffic, and the clustering used synthetic data.
3. Models trained on foreign datasets transfer imperfectly to Malaysian roads and phone photos ([Kavcı & Cansız, 2024](https://doaj.org/article/dc5dd3ba78e6437d85a2330b70c493fa)).
4. No description found of showing officers the reasons behind each score, or of an officer review and repair-tracking workflow around it.

## Project Objectives

- **O1:** To develop and evaluate a computer-vision model for potholes and three crack types using public datasets, tested on local phone photos.
- **O2:** To design and evaluate duplicate-report grouping and an explainable risk-based priority recommendation using image similarity, GPS, timestamps and damage information.
- **O3:** To develop a dashboard that maps incidents, recommends priority, and supports officer review and repair tracking.

## Target Users

Township and council maintenance officers (primary), repair crews, residents who report damage, and supervisors monitoring backlog.

## Data Sources

| # | Source | URL |
|---|---|---|
| 1 | RDD2022 dataset (Figshare) | https://figshare.com/articles/dataset/RDD2022_-_The_multi-national_Road_Damage_Dataset_released_through_CRDDC_2022/21431547 |
| 2 | RDD2022 paper | https://arxiv.org/abs/2209.08538 |
| 3 | JKR complaint channels | https://www.thevibes.com/articles/news/11597/jkr-gives-11-ways-to-channel-complaints-after-kj-pothole-uproar |
| 4 | Aberdeenshire road defect scoring (priority factors) | https://www.aberdeenshire.gov.uk/media/28117/roadinspectionsummary.pdf |

## Comparison with MYJalan

**Similar:** Both let residents report road damage with a photo and GPS location and then track the repair status.

**Different:** InfraManage detects the damage type from the photo, groups duplicate reports into one incident, and recommends an explainable priority, whereas MYJalan's described AI is only speech-to-text for filing complaints.

## Responsible AI Risks

| Risk | Description | Mitigation |
|---|---|---|
| Unreliable detection | A hazard could be missed or ranked low | Confidence thresholds, officer review, local accuracy reporting |
| Fairness | Areas that report more could get faster repairs | Score on road type, damage and traffic, not report volume; audit response times by area |
| Privacy | Photos can capture faces, number plates and homes; GPS reveals reporters' locations | Blur or reject identifiable content; store minimal personal data |
| Wrongly merged reports | Two nearby potholes could be grouped as one | Every photo is kept in the incident; an officer can split it |
