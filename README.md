# hip-SL
Adaptation of the emer/leabra (github.com/emer/leabra) hippocampus model for statistical learning

### Description
This repository contains an updated version of the Schapiro et al. (2017) statistical learning hippocampus model, originally written in C++ emergent (www.grey.colorado.edu/emergent/index.php/Main_Page).
The model has been re-written for the Golang emergent (www.github.com/emer/emergent) framework and is based on the emer/leabra/examples/hip hip.go example.

### Usage instructions
1. Install Golang.
2. Install emergent by following the instructions at www.github.com/emer/emergent/wiki/Install.
3. Download/Clone this repository.
4. `cd` to the repo folder and run the command `go build && hip-sl`.

This should open the GUI view for the model. Please refer to emergent documentation for information on the GUI view.

### Parameter differences between the hip.go example and hip-SL.go
All parameter changes are listed in the `hip.go_vs_hip-SL.go_param_changes.xlsx` file.

### Architecture differences between the C++ emergent version and hip-SL.go
1. KWTA inhition has been replaced by FFFB inhibition. For more information see: www.grey.colorado.edu/CompCogNeuro/index.php/CCNBook/Networks
2. Learning rates for MSP and TSP have been changed for better performance:

| Learning Rate | C++ model     | Golang model  |
| ------------- |:-------------:|---------------|
| MSP    	| 0.02		| 0.05 		|
| TSP     	| 0.2      	| 0.4 		|

3. Golang emergent divides trials into four quarters of 25 cycles each, with each quarter serving as a different learning phase. The ActMid, ActM and ActP learning variables from C++ emergent are therefore recorded at different timepoints in a Golang emergent training trial vs a C++ emergent training trial. Cycle at which each variable is recorded for the two models:

| 			| ActMid | ActM | ActP |
|---------------	|----	 | ---	| ---  |
| C++ model	| 40	 | 80 | 100   |
| Golang model	| 25	 | 75   | 100   |

Note: Training stimuli presentation has also been tweaked for better performance. AB pair presentation strengths at Input:

| 			| A | B |
|---------------	|----	 | ---	|
| C++ model 	| 0.9	 | 0.95	|
| Golang model 	| 0.8	 | 0.95   |

### Differences in results between the C++ emergent version and hip-SL.go
The only observed qualitative change in results is the lack of a checkerboard pattern (see Schapiro et al. 2017) in the 'Initial Response' heatmap for CA1.

Please see https://github.com/schapirolab/hip-sl/wiki/Results for full results.
