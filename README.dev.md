Thanks again for your interest in using Cloud TPUs to accelerate your machine learning research. Your Google Cloud project [tokyo-carving-231908](https://notifications.google.com/g/p/ADa0GC8Ep8t-qdNd77T4D9EDQr-fwHOwCKOYLS0mDj4njUbRI8g4le7EyZtt2C3_zRDeKhvEjebeyvgR7wIHSkvo_S5zgGi6sRo1ECEI8Gon3U28zgxFR6lUaqj3No_d3MdAqUcPCbOqLylcQZ4CbV63az2T8mvSijdhRd70jv16W8eP_fZZGh727rLJgyfal8JGonoR_PWWciOq4byYggrm6k0p--qTNd7PphHUv92wIOQhJ3OVKL73hPHC) now has access to the following quota free of charge for 60 days:

**5 on-demand Cloud TPU v3-8 device(s) in zone europe-west4-a**

**100 preemptible Cloud TPU v2-8 device(s) in zone us-central1-f**

**5 on-demand Cloud TPU v2-8 device(s) in zone us-central1-f**

```
bash infra/spin-up-vm.sh levanter1 -z us-central1-f -t v2-8\

gcloud compute tpus tpu-vm scp --recurse levanter/ levanter1:/home/vlialin/ --zone $ZONE --worker=all

export NAME=levanter1
export ZONE=us-central1-f
gcloud compute tpus tpu-vm ssh \
    $NAME --zone $ZONE --worker=all \
    --command 'WANDB_API_KEY=... levanter/infra/run.sh python levanter/src/levanter/main/train_lm.py --config_path levanter/config/gpt2_small.yaml --trainer.checkpointer.base_path gs://vlialin-levanter'
```


Some other commands:

```
# create 2.8
gcloud compute tpus tpu-vm create node-1-tpu2-8 \
	--zone=us-central1-f \
	--accelerator-type=v2-8 \
	--version=tpu-vm-base

# connect 2.8
gcloud compute tpus tpu-vm ssh node-1-tpu2-8 --zone us-central1-f

# stop
gcloud compute tpus tpu-vm stop node-1-tpu2-8 --zone=us-central1-f

# start
gcloud compute tpus tpu-vm start node-1-tpu2-8 --zone=us-central1-f

# scp the levanter
cd ~/Documents
gcloud compute tpus tpu-vm scp --recurse levanter/ levanter1:/home/vlialin/ --zone $ZONE --worker=all

#ssh
# Same commands, but for 3.8 and europe-west4-a
#
# create 3.8
gcloud compute tpus tpu-vm create node-1-tpu3-8 \
	--zone=europe-west4-a \
	--accelerator-type=v3-8 \
	--version=tpu-vm-base

# connect 3.8
gcloud compute tpus tpu-vm ssh node-1-tpu3-8 --zone us-central1-f
```