Project Name	InfraManage
Domain	Smart township and municipal infrastructure maintenance (initial focus: road damage)
Problem Statement	Maintenance teams receive damage reports as scattered photos and messages, with no consistent way to tell what the damage is, whether it was already reported, or how urgent it is. Road users, especially motorcyclists, bear the risk and repair costs. AI can detect the damage type from photos, group duplicate reports into one incident using image similarity and location, and recommend an explainable priority, with officers keeping the final decision.
Evidence of the Problem	Evidence 1: JKR patched 168,003 potholes in 2020 along 14,385 km of federal roads, and over 55,800 potholes were reported in 2024.
Source: FMT (2021); RinggitPlus
Evidence 2: Reporting is fragmented. JKR listed 11 complaint channels, and the public accused it of responding fast only when a minister was affected.
Source: The Vibes; The Rakyat Post
Evidence 3: Police statistics cited by a MIROS board member recorded 55 deaths from pothole-related crashes in 2018, plus 16 serious and 40 minor injuries. This was about 0.88% of national road fatalities, so potholes are a small but preventable, maintenance-related share. The data doesn’t say whether crashes were on federal or local roads.
Source: The Vibes (Shahrim Tamrin)
Evidence 4: In January 2021 a senior citizen on a motorcycle died after hitting potholes on Jalan Tengah near Mid Valley, Kuala Lumpur.
Source: The Vibes (Shahrim Tamrin)
Evidence 5: Duplicate reports cost municipalities money, and authorities often still check for duplicate or fake reports and rate severity by hand, causing delays and a growing backlog.
Source: Zhang & Wang (2015); Salcedo et al. (2022)
Initial Related Work (at least 3)	1. RDD2022 (Arya et al.): 47,420 images from six countries, with over 55,000 annotated damages in four types.
Source: arXiv
Limitation: Malaysia is not among the six countries, and it covers detection only.
2. Sharma et al., road monitoring pilot: YOLOv8 got an F1 of 0.45 during fine-tuning, and professionals rated 65% of images satisfactory or better.
Source: TRID
Limitation: real-world detection is far below benchmark scores, with confusion between similar-looking objects.
3. Salcedo et al. (2022), prioritisation from crowdsourced reports: road segmentation, YOLOv5 detection (single cracks, crocodile cracks, potholes), image-based duplicate matching (SIFT and FLANN, about 85% precision) and location clustering with a weighted-sum priority.
Source: J. Sens. Actuator Netw.
Limitation: duplicates use images only (no GPS or time), priority counts damage types only, clustering was tested on synthetic data, and traffic density is left as future work.
4. Aberdeenshire Council, risk-based defect scoring: scores a pothole by its position on the road, size and the road’s speed limit, then assigns a repair priority.
Source: Aberdeenshire Council
Limitation: a manual inspector process, with no automatic photo analysis.
5. MYJalan app: GPS tagging, photo upload and status tracking.
Source: Borneo Post
Limitation: no automatic damage classification or risk scoring described.
Engineering Gap / Limitation	Earlier work already combines parts of this pipeline (Salcedo et al.), so the gap is in how well it fits a real township workflow:
1. Duplicate matching there uses images only, while InfraManage also uses GPS and timestamps.
2. Priority there counts damage types and ignores road type and traffic, and the clustering used synthetic data.
3. Models trained on foreign datasets transfer imperfectly to Malaysian roads and phone photos (Kavcı & Cansız, 2024).
4. I found no description of showing officers the reasons behind each score, or of an officer review and repair-tracking workflow around it.
Initial Project Objectives	O1: To develop and evaluate a computer-vision model for potholes and three crack types using public datasets, tested on local phone photos.
O2: To design and evaluate duplicate-report grouping and an explainable risk-based priority recommendation using image similarity, GPS, timestamps and damage information.
O3: To develop a dashboard that maps incidents, recommends priority, and supports officer review and repair tracking.
Target Users	Township and council maintenance officers (primary), repair crews, residents who report damage, and supervisors monitoring backlog.
Data Sources (at least 2)	Source 1: RDD2022 dataset (Figshare). URL: https://figshare.com/articles/dataset/RDD2022_-_The_multi-national_Road_Damage_Dataset_released_through_CRDDC_2022/21431547
Source 2: RDD2022 paper. URL: https://arxiv.org/abs/2209.08538
Source 3: JKR complaint channels. URL: https://www.thevibes.com/articles/news/11597/jkr-gives-11-ways-to-channel-complaints-after-kj-pothole-uproar
Source 4: Aberdeenshire road defect scoring (for priority factors). URL: https://www.aberdeenshire.gov.uk/media/28117/roadinspectionsummary.pdf
Similar to MYJalan	Both let residents report road damage with a photo and GPS location and then track the repair status.
Different from MYJalan	InfraManage detects the damage type from the photo, groups duplicate reports into one incident, and recommends an explainable priority, whereas MYJalan’s described AI is only speech-to-text for filing complaints.
Responsible AI Risks (at least 2)	Risk 1, Unreliable detection: a hazard could be missed or ranked low. Mitigation: confidence thresholds, officer review and local accuracy reporting.
Risk 2, Fairness: areas that report more could get faster repairs. Mitigation: score on road type, damage and traffic, not report volume, and audit response times by area.
Risk 3, Privacy: photos can capture faces, number plates and homes, and GPS reveals reporters’ locations. Mitigation: blur or reject identifiable content and store minimal personal data.
Risk 4, Wrongly merged reports: two nearby potholes could be grouped as one. Mitigation: every photo is kept in the incident, and an officer can split it.
