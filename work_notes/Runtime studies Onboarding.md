Goal: 
Study runtime in dependence of number of GPUs and image/dataset size on GCP and Exaion.

Method: 
1.) Use main runscript and run the setup with all relevant combinations of:
	- num GPUs [1,2,4,8]
	- train batch size
	- image size, input_dim unet
	- CelebA, LSUN

2.) Inspect total runtime for all these scenarios. 
3.) Add to this spreadsheet https://docs.google.com/spreadsheets/d/1WH-qUWZnaEu1boMGOv6xRPd4cRVk3RQK_q2ZHWfeUeU/edit#gid=1670100809 & share on Confluence https://1qbit-intra.atlassian.net/wiki/spaces/MLD/pages/2739863620/Timing+Studies#GCP-V100-vs-Exaion-P100

Details & Notes:
- development branch: `timing_benchmarks_add_dataset_handling`
- shell script with relevant commands: `./221102_runtime_studies_gcp_exaion_platforms.sh`
	- two sets of commands - for GCP (plain python) and for Exaion (docker)
	- docker command mounts the local directory using `-v pwd:/workspace`
	- that local directory shoud point to a local version of the development branch
- data: please run the celeba and lsun data download scripts as a cross check - they should add each dataset to `./data/`
- adjust configuration files to run on CelebA and LSUN
- in issue XYZ we can collect which combination of batch size and image size works depending on the 16GB GPU memory
- spreadsheet & confluence contain additional information