ssh -p 2222 admsrv@163.114.159.73 -i ~/.ssh/id_ed25519_1qbit


ssh -p 31122 admsrv@91.239.56.145 -i ~/.ssh/id_ed25519_1qbit
scp -p 31122 admsrv@91.239.56.145 -i ~/.ssh/id_ed25519_1qbit 


python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128
docker run --gpus 0 --ipc=host --memory=20g -it -v `pwd`:/workspace quay.io/1qbit/diffusion-models:base-devel bash -c "python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128"

python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128
docker run --gpus 1 --ipc=host --memory=20g -it -v `pwd`:/workspace quay.io/1qbit/diffusion-models:base-devel bash -c "python tests/profiling/generate_synthetic_images_timing.py --num_gpu 1 --train_batch_size 128"


https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

git clone https://github.com/1QB-Information-Technologies/Diffusion-models.git
Copy & paste PAT as password

add to ssh

```
Host exaion_a6000
   HostName exaion_a6000

Host exaion_a6000
   HostName 163.114.159.73
   User admsrv
Port 2222

   IdentityFile ~/.ssh/id_ed25519_1qbit

   IdentitiesOnly yes
```

mkdir eric

 rsync -avz -P --port=2222 -e "ssh -p 2222 -i $HOME/.ssh/id_rsa" test2 admsrv@163.114.159.73:~/


ssh -p 2222 admsrv@163.114.159.73 -i ~/.ssh/id_ed25519_1qbit -L 5000:localhost:5000

docker exec -it b8f22cdf95de bash
python applications/synthetic_image_generation/ddpm_image_generation.py 

make up
docker ps

docker -> mounting shared data directory

 rsync -avz -P --port=2222 -e "ssh -p 2222 -i $HOME/.ssh/id_rsa" admsrv@163.114.159.73:~/data/padchest_reduced_221208 .


rsync -avz -P --port=31122 -e "ssh -p 31122 -i $HOME/.ssh/id_ed25519" /home/admsrv/eric/Diffusion-models/model_checkpoints_benchmark_221216_v01_256 admsrv@91.239.56.145:~/data/. 

ssh -p 31122 "ssh -p 2222 -i $HOME/.ssh/id_ed25519" admsrv@91.239.56.145 -i ~/.ssh/id_ed25519_1qbit