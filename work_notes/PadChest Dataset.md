# PadChest Dataset
Pathology Detection in Chest radiographs


Source:
https://bimcv.cipf.es/bimcv-projects/padchest/

Kaggle Sample:
https://www.kaggle.com/datasets/raddar/padchest-chest-xrays-sample

Original Paper: 
https://arxiv.org/abs/1901.07441v1

Repositories:
- preprocessing chest datasets in front/side view: https://github.com/xinario/chestViewSplit 

https://1qbit-intra.atlassian.net/wiki/spaces/MLD/pages/2790522997/PadChest+Preparation


Sample size: 160000
- 6 different views:
	- standard PA
	- standard L (lateral)
	- AP vertical or erect
	- AP horizontal or supine
	- pediatric
	- rib views.
- labels: 
	- 174 radiographic findings
	- 19 differential diagnoses (TODO)
	- 104 anatomic locations
- 27% manually annotated, 73% annoptated using a DNN trained on the manually annotated (ground truth)
- standardized labelling language (Unified Medical Language System (UMLS))

Reference work:
- ChestX-Ray8 - CNN to classify and localize 8 pathologies
- ChestX-Ray14 - CNN to classify and localize 14 pathologies

Other Datasets:
- NIH repo (112000 images, all front view, 14 labels)
- Korean Institute repo - Tubercolisis (10900, 3000 positive tubercolosis)
- Indiana Uni - 7470 frontal and lateral chest xray images

Relevant pitfalls:
- presence of artifacts/external features in images: 
	- tubes, cathethers, life-support devices 
- patient position
- unbalanced presence of entities (like pathologies)
- dataset sizes, in particular when looking at specific labels

- x-ray projections:
	- P-A (posterior-anterior - back to front)
	- A-P (anterior- posterior -  front to back)
	- supine: lying down
	- lateral - from the side
	- lordotic - leaning back, extending lumbar spine
	- decubit - lying sideways, arm up
	- 
Preprocessing:
- 

- other notes: 
	- projection information is highly relevant for diagnosis
		- different views might reveal organs, air pockets etc which could be picked up as anomaly
	- 

GLOSSARY:
- DICOM - Digital Imaging and Communications in Medicine image standard (*.dcm)
