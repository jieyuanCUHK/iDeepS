# iDeepS
iDeepS aims to discover Sequence-Structure Motifs, it trains deep learning models to infer binding sequence and structure motifs from sequences simultaneously.
We first encode the sequence and secondary structure into one-hot encoding, which are further fed into CNNs to learn abstract motif features. 
then we use bidirectional LSTM to capture the long range dependencies between binding sequence and structure motifs identified by CNNs.
Finally the learned abstract features are fed into classification layer to predict RBP binding sites on RNAs.
We comprehensively evaluate iDeepS on verified RBP binding sites derived from large-scale representative CLIP-seq datasets.


# Dependency <br>
<a href=https://github.com/fchollet/keras/>keras 1.1.2 library</a> <br>
<a href=https://github.com/scikit-learn/scikit-learn>sklearn</a> <br>
<a href=https://github.com/fabriziocosta/EDeN>EDeN</a> <br>
<a href=https://bibiserv.cebitec.uni-bielefeld.de/download/tools/rnashapes.html>RNAshapes</a> <br>

# Content <br>
./datasets: the training and testing dataset with sequence and label indicating it is binding sites or not<br>
./motif/seq_cnn: detected binding sequence motifs from iDeepS, and we also report the matched known motifs uusing TOMTOM and motif enrichment analysis using AMD in MEME Suite. <br>
./motif/structure_cnn: detected binding structure motifs from iDeepS. It also reports the motif enrichment analysis using AMD in MEME Suite<br>
./ideeps.py: the python code, it can be ran to reproduce our results. <br>


# Usage

 python ideeps.py [-h] [--data_file <data_file>] [--train TRAIN] <br>
                [--model_dir MODEL_DIR] [--predict PREDICT] <br>
                [--out_file OUT_FILE] <br>
                [--motif MOTIF] [--batch_size BATCH_SIZE] <nr>
                [--n_epochs N_EPOCHS] <br> <br>
where the input training file should be sequences.fa.gz

# Use example
<b>1.</b> Train the model using your data (currently only support fix-length sequences): <br>
python ideep.py --train=True --data_file=datasets/clip/10_PARCLIP_ELAVL1A_hg19/30000/training_sample_0/sequences.fa.gz --model_dir=models
<br> <br>
--model_dir: the dir used to save the trained model, which is used for prediction step. <br>
 --data_file: the <b>training</b> sequence file sequences.fa.gz with label informaiton in the head. <br>
<br>
<b>2.</b> predict the binding probability for your sequences (you need use the same dir for saved models in training step): <br>
 python ideep.py --predict=True --data_dir=datasets/clip/10_PARCLIP_ELAVL1A_hg19/5000/test_sample_0/sequences.fa.gz --model_dir=models --out_file=YOUR_OUTFILE
<br> <br>
--model_dir: The saved dir for models in training step. <br>
--data_file: configure your <b>testing</b> sequence file sequences.fa.gz.

<br><br> 

Contact: Xiaoyong Pan (xypan172436atgmail.com)
