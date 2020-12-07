

# MLSys'21 Additional Rebuttal Material (submisson #170)

We provide supplementary material that wouldn't be possible to include in the format used in the rebuttal document. The content here provided supports the claims made in the rebuttal addressing the points raised by reviewers.


## Federated ResNet18 learning on Heterogenous Clients with Flower

Flower enables deploying FL workloads on edge devices. Achieving this with other frameworks that by design are limited to simulating these FL experiments, would require a substantial engineering effort for individual researchers. 

With Flower we can obtain metrics that wouldn't be possible to get from simulations alone. For instance, power consumption and accurate latency metrices at each node. 


![image](media/ResNet18_federated.png)

The figure above shows two FL experiments using two NVIDIA-Jetson devices as clients. Both experiments train a ResNet18 on CIFAR-10 for 5 rounds. We run this experiment twice: first, using the high performance mode available on each device (see blue and oragne lines); and a lower power mode (purple and green lines). The power monitoring was done by running on a parallel process the `tegrastats` utility function available on these devices.

<<Takeaways from the figure>>