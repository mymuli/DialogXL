# DialogXL
This repo contains the PyTorch implementaion for AAAI-2021 accepted paper DialogXL: All-in-One XLNet for Multi-Party Conversation Emotion Recognition.

For any questions about the implementation, plaese email shenwzh3@mail2.sysu.edu.cn.

## Requirements
* Python 3.6
* PyTorch 1.4.0
* [Transformers](https://github.com/huggingface/transformers) 3.0.2
* scikit-learn 0.23.1
* CUDA 10.0

## Perparation

### Datasets
We have provided the preprocessed datasets of IEMOCAP, MELD, DailyDialog and EmoryNLP in `/data/`. For each dataset, there is 3 json files containing dialogs for train/dev/test set. Each dialog contains utterances
 and their corresponding speaker information and emotion labels.
 
### Pre-trained XLNet
You should download the pytorch version pre-trained 
`xlnet-base` model and vocabulary from the link provided by huggingface. 
Then change the value of parameter `--bert_model_dir` and `--bert_tokenizer_dir` to the directory of the bert model.

## Evaluate
You can download our well-trained DialogXL for each dataset from 
https://drive.google.com/drive/folders/1ONGBbo9r9S49i5bz4jgrC79txQHNVZv2?usp=sharing
or https://pan.baidu.com/s/1SYbpCI4LTzUnYbRKzPvijg 提取码 jpfe

Then put them to `/DialogXL/saved_models/`

You can run the following codes to get results very close to those reported in our paper (we report the average of 5 random runs in paper):

For IEMOCAP (test F1: 65.88): 
`python eval.py --dataset_name IEMOCAP --max_sent_len 200 --mem_len 900 --windowp 10 --num_heads 2 2 4 4 --modelname IEMOCAP_xlnet_dialog`

For DailyDialog (test F1: 55.67): 
`python eval.py --dataset_name DailyDialog --max_sent_len 300 --mem_len 450 --windowp 10 --num_heads 1 2 5 4 --dropout 0.3 --modelname DailyDialog_xlnet_dialog
`

For EmoryNLP (test F1: 36.27): 
`python eval.py --dataset_name EmoryNLP --max_sent_len 150 --mem_len 400 --windowp 5 --num_heads 1 2 4 5 --modelname EmoryNLP_xlnet_dialog`


## Training
You can also train the models with the following codes:

For IEMOCAP: 
`python run.py --dataset_name IEMOCAP --max_sent_len 200 --mem_len 900 --windowp 10 --num_heads 2 2 4 4 --dropout 0 --lr 1e-5 --epochs 50`

For DailyDialog: 
`python run.py --dataset_name DailyDialog --max_sent_len 300 --mem_len 450 --windowp 10 --num_heads 1 2 5 4 --dropout 0.3 --lr 1e-6 --epochs 20`

For EmoryNLP: 
`python run.py --dataset_name EmoryNLP --max_sent_len 150 --mem_len 400 --windowp 5 --num_heads 1 2 4 5 --dropout 0 --lr 7e-6 --epochs 10`

