# Librispeech example

We assume that you have run the Kaldi [Librispeech recipe](https://github.com/kaldi-asr/kaldi/blob/master/egs/librispeech/s5/run.sh) up to the end of GMM stages. You also need to build the denominator graph for sequence training. 

## CE training

The top-level script for CE training is "run\_ce.sh", which is like 

  ```
    python ../../bin/train_ce.py -config configs/ce.yaml \
    -data configs/data.yaml \
    -exp_dir exp/tr460_blstm_3x512_dp02 \
    -lr 0.0001 \
    -batch_size 1 \
    -sweep_size 460 \
    -aneal_lr_epoch 3 \
    -num_epochs 8 \
    -aneal_lr_ratio 0.5 
  ```
The ce.yaml file contains the data and model configurations. The data.yaml file contains the data, which are raw waveforms, and labels. The data.yaml in the above example is like

  ```
   clean_source:                                                            
  1:                                                                     
    type: Librispeech                                                    
    wav: /datadisk2/lial/LibriSpeechWav/train-clean-100.zip              
    label: /datadisk2/lial/LibriSpeechWav/train-960-pdf-ids.txt          
    aux_label: /datadisk2/lial/LibriSpeechWav/train-960-trans-ids.txt    
  2:                                                                     
    type: Librispeech                                                    
    wav: /datadisk2/lial/LibriSpeechWav/train-clean-360.zip              
    aux_label: /datadisk2/lial/LibriSpeechWav/train-960-trans-ids.txt    
    label: /datadisk2/lial/LibriSpeechWav/train-960-pdf-ids.txt          
  3:                                                                     
    type: Librispeech                                                    
    wav: /datadisk2/lial/LibriSpeechWav/train-other-500.zip              
    aux_label: /datadisk2/lial/LibriSpeechWav/train-960-trans-ids.txt    
    label: /datadisk2/lial/LibriSpeechWav/train-960-pdf-ids.txt
  ```


