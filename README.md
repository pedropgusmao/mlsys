

# MLSys'21 Additional Rebuttal Material (submission #170)

We provide supplementary material that wouldn't be possible to include in the format used in the rebuttal document. The content here provided supports the claims made in the rebuttal addressing the points raised by reviewers.


## Federated ResNet18 learning on Heterogenous Clients with Flower

Flower enables deploying FL workloads on edge devices. Achieving this with other frameworks that by design are limited to simulating these FL experiments, would require a substantial engineering effort for individual researchers. 

With Flower we can obtain metrics that wouldn't be possible to get from simulations alone. For instance, power consumption and accurate latency metrices at each node. 

<img src="https://user-images.githubusercontent.com/847743/101476321-7bf34800-3945-11eb-9650-c4060352c1a5.png">

Anonymized link to Power Consumption and Timings (click to reveal the figure):
![image](media/ResNet18_federated.png)

The image above summarizes the two FL experiments we ran using two NVIDIA-Jetson devices as clients. Both experiments train a ResNet18 on CIFAR-10 for 5 rounds. We run this experiment twice: first, using the high performance mode available on each device (see blue and oragne lines); and a lower power mode (purple and green lines). The power monitoring was done by running on a parallel process the `tegrastats` utility function available on these devices.


We report below the average time and total power consumption (on-device training+communication+aggregation) per round for each device in each power configuration.

### High Power Consumption mode


```
+-------------------------+--------------------------------+---------------+------------------+
|         Device          | Train time per epoch (s/epoch) | Avg.(s/epoch) | Total Energy (KJ)|
+-------------------------+--------------------------------+---------------+------------------+
| Xavier-NX (15W-6cores)  | [191, 170, 168, 169, 171]      |         173.6 |        7.4       |
| Jetson-TX2 (15W-6cores) | [274, 270, 271, 272, 270]      |         271.4 |       11.1       |
+-------------------------+--------------------------------+---------------+------------------+
```

### Low Power Consumption mode
```
+--------------------------+--------------------------------+---------------+------------------+
|          Device          | train time per epoch (s/epoch) | Avg.(s/epoch) | Total Energy (KJ)|
+--------------------------+--------------------------------+---------------+------------------+
| Xavier-NX (10W-4cores)   | [210, 203, 197, 201, 204]      |           203 |        5.6       |
| Jetson-TX2 (7.5W-4cores) | [390, 380, 382, 377, 382]      |         382.2 |        7.6       |
+--------------------------+--------------------------------+---------------+------------------+
```

###  CIFAR10 Training times on Raspberry Pi devices

Using the same setup as the above, we ran a similar experiment on two different generations of Raspberry Pi's (3 and 4), using a batch size of 64 samples, to measure the speed-up in processing time accross different generations.
This example shows Flower's capability of distinguishing between on-device compute time and communication+aggregation times.

```
+----------------+------------------------------------------+-----------------+
|     Device     | Average compute time per epoch (s/epoch) | Comm.+Aggr. (s) |
+----------------+------------------------------------------+-----------------+
| Raspberry Pi 3 |                                      298 |               6 |
| Raspberry Pi 4 |                                      256 |               4 |
+----------------+------------------------------------------+-----------------+
```


## Federated Learning with 10k clients

We further show Flower's scalability by training on CIFAR10 dataset using **10 thousand** clients with **1 thousand** participating clients in each run for a few epochs. The Figures below show the accuracies and losses obtained after each trained round.

Accuracy:

<img src="https://user-images.githubusercontent.com/847743/101476644-020f8e80-3946-11eb-96ae-943a34e2b9fd.png">

Anonymized link to Flower Accuracy using 10K clients (click to reveal the figure): 
![image](media/flwr_cifar10_10k_accuracy.png) 


Loss:

<img src="https://user-images.githubusercontent.com/847743/101476812-371be100-3946-11eb-8209-14d29a176dfc.png">

Anonymized link to Flower Loss using 10K clients (click to reveal the figure): 
![image](media/flwr_cifar10_10k_loss.png)

Each round consisted of one epoch and about 90GB of data were transmitted during each round. *FedAvg* was used to generate the results.  


