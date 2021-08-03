# Variable-Length-Piano-Infilling
The official implementation of Variable-Length Piano Infilling (VLI). (paper: Variable-Length Music Score Infilling via XLNet and Musically Specialized Positional Encoding)

VLI is a new Transformer-based model for music score infilling, i.e., to generate a polyphonic music sequence that fills in the gap between given past and future contexts. Our model can infill a variable number of notes for different time spans. 

## Installation
1. Clone and install the modified [Huggingface Transformer](https://github.com/reichang182/Transformer) package.
2. Clone this repo and install the required packages.
```
git clone https://github.com/reichang182/Variable-Length-Piano-Infilling.git
cd  Variable-Length-Piano-Infilling
pip install -r requirement.txt
```
3. Download and unzip the AIlabs.tw Pop1K7 dataset. (Download link: [here](https://drive.google.com/file/d/1qw_tVUntblIg4lW16vbpjLXVndkVtgDe/view?usp=sharing)).

## Training & Testing
	# Prepare data
	python prepare_data.py \
		--midi-folder datasets/midi/midi_synchronized/ \
		--save-folder ./
	
	# Train the model
	python train.py --train

	# Test the trained model
	python train.py
	
## Baselines
The codes to run baselines in our paper are in the ```baselines``` folder.
We implement ILM and FELIX according to their paper ([ILM](https://arxiv.org/abs/2005.05339) and [FELIX](https://arxiv.org/abs/2003.10687)) and based on the implementation of Transformer-XL and BERT in [Huggingface Transformer](https://github.com/reichang182/Transformer).
They can also be trained and tested through the same command as our model does above.
	
	# cd baselines/ILM or cd baselines/FELIX
	
	# Train the model
	python train.py --train \
		--dict-file ../../dictionary.pickle
		--data-file ../../worded_data.pickle
	
	# Test the trained model
	python train.py \
		--dict-file ../../dictionary.pickle
		--data-file ../../worded_data.pickle

## Architecture
<img src="figures/architecture.png" alt="drawing" width="600"/>

## Results
<figure>
  <img src="figures/training_loss.png" alt="drawing" width="600"/>
  <figcaption>The training NLL-loss curves of ours and baseline models.</figcaption>
</figure>
<img src="figures/metric_difference.png" alt="drawing" width="600"/>
<figure>	
  <img src="figures/subjective_evaluation.png" alt="drawing" width="600"/>
  <figcaption>Results of the user study: mean opinion scores in 1–5 in M(melodic fluency), R(rhythmic fluency), I(im-pression), and percentage of votes in F(favorite), from ‘all’ the participants or only the music ‘pro’-fessionals.</figcaption>
</figure>
