# A Secure and Efficient Wireless Charging Scheme for Electric Vehicles in Vehicular Energy Networks

Implementation of **"A Secure and Efficient Wireless Charging Scheme for Electric Vehicles in Vehicular Energy Networks" (submitted to IEEE TVT).**

## Introduction
In our paper, we propose **a secure and privacy-preserving wireless charging (SPC) framework for collaborative wireless energy transfer in Vehicular Energy Networks (VENs)** which can achieve the following three goals:
- **Decentralized privacy provisioning**: a consortium blockchain-based personal data management mechanism is presented for EV users to allow only designated entities can process their personal rating information. The blockchain platform serves as a trust-free authentication and authorization server by issuing *access token* as a ``proof-of-permission".
- **Distributed trust management**: with the shared rating information, a trust model in the blockchain context is constructed from explicit and implicit trust computing to assess the trustworthiness of energy nodes and identify malicious entities in providing energy services.
- **Cooperative energy transfer**: by introducing *cooperative wireless energy transfer (CWET) mode*, we analyze the utilities for charging EVs, discharging EVs, and energy nodes with diverse user characteristics. Furthermore, the interactions among the three entities are modeled as a *game-based three-tier energy scheduling problem*. In the first tier, cooperative charging and discharging EVs select the optimal energy demand and price strategies based on the Stackelberg game. In the second tier, the stable matching pairs for charging and discharging EVs are obtained through the V2V matching game. In the third tier, matched EV pairs determine their optimal candidate energy node to realize inter-vehicle wireless energy transfer by the reverse auction game.

## Getting Started
The **[Hyperledger Caliper](https://www.hyperledger.org/use/caliper)**, which is a widely used performance benchmark, is employed to implement our blockchain system. The Caliper adaptor is programmed using Node.js and Fabric Client SDK to interact with the blockchain platform. Caliper is published as the @hyperledger/caliper-cli NPM package, providing a single point of install for every supported adapter.

**[Eclipse SUMO](https://sumo.dlr.de/docs/index.html)** (Simulation of Urban MObility), an open source, highly portable, microscopic and continuous multi-modal traffic simulation package designed to handle large networks. SUMO allows modelling of intermodal traffic systems including road vehicles, public transport and pedestrians. Included with SUMO is a wealth of supporting tools which handle tasks such as route finding, visualization, network import and emission calculation. SUMO can be enhanced with custom models and provides various APIs to remotely control the simulation.

Pre-requisites：
- node-gyp, python2, make, g++ and git (for fetching and compiling some packages during install)
- Node.js v8.X LTS or v10.X LTS (for running Caliper)
- Docker and Docker Compose (only needed when running local examples, or using Caliper through its Docker image)
- [SUMO v1.10.0](https://sumo.dlr.de/docs/Downloads.php) 

Get the source code, and install all the dependencies.

```bash
git clone --recursive https://github.com/Yentl-Wang/Vehicular-Energy-Network

pip install -r requirements.txt
```

## Experiments on blockchain
We utilize the SUMO simulator to generate a simulation scenario on the map of a 2km * 2km urban area in Belo Horizonte. The vehicular traces of EVs are obtained from a modified public data set [Vehicular Trace](http://www.prof.rettore.com.br/vehicular-trace/). 

For the blockchain system in the Caliper benchmark, we use the following three metrics: *throughput*, *latency*, and *scalability*. Besides, we evaluate the metric *Secure energy transfer ratio* to validate the performance of reputation model, which is defined as the ratio of wireless energy transmission with legitimate energy nodes to the total amount of traded energy of EVs.

## Simulations on game model

There are 29 energy nodes deployed on the road segments to deliver DWPT services and 4 RSUs to offer V2R communication services for EVs. There are 140 EVs driving on the roads, and the ratios of charging EVs and discharging EVs are equal to 0.5. The SoC of charging EVs is evenly distributed within [20%, 49%], while that of discharging EVs is evenly selected in [50%, 90%]. The minimum SoC of EV is set as 20%. The satisfaction parameter of charging EVs follows a uniform distribution between 20 and 60. The upper and lower bound of the cost for energy transfer service are set as 2.5 cents and 10 cents, respectively. 

We define the following metrics to evaluate the performance of the proposed scheme in terms of efficiency.
- Average utility of matched charging EVs (AUC): the total utility of charging EVs in the stable matching divided by the number of matched EV pairs.
- Average utility of matched discharging EVs (AUD): the total utility of discharging EVs in the stable matching divided by the number of matched EV pairs.
- Satisfactory EV charging ratio: It is defined by <a href="https://www.codecogs.com/eqnedit.php?latex={M_{sat}}/M&space;\times&space;100\%" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{M_{sat}}/M&space;\times&space;100\%" title="{M_{sat}}/M \times 100\%" /></a>, where <a href="https://www.codecogs.com/eqnedit.php?latex={M_{sat}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{M_{sat}}" title="{M_{sat}}" /></a> is the number of charging EVs whose energy demand has been fully satisfied in a certain time period, and M is the total number of charging EVs in that time period. Here, the time period used in simulation is the energy scheduling time of our proposed GTS algorithm.
- Unhappiness index: It is defined as the number of unhappy EV pairs in a matching, which also indicates the instability of the matching. For an unhappy EV pair (m,n), it satisfies: 1) <a href="https://www.codecogs.com/eqnedit.php?latex=m{&space;\succ&space;_n}\Psi(n)\,{\text{and}}\,&space;n{&space;\succ&space;_{m}}\Psi(m)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m{&space;\succ&space;_n}\Psi(n)\,{\text{and}}\,&space;n{&space;\succ&space;_{m}}\Psi(m)" title="m{ \succ _n}\Psi(n)\,{\text{and}}\, n{ \succ _{m}}\Psi(m)" /></a>, or 2) <a href="https://www.codecogs.com/eqnedit.php?latex=m{&space;\succ&space;_n}\Psi(n)\,{\text{and}}\,&space;\Psi(m)=\emptyset" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m{&space;\succ&space;_n}\Psi(n)\,{\text{and}}\,&space;\Psi(m)=\emptyset" title="m{ \succ _n}\Psi(n)\,{\text{and}}\, \Psi(m)=\emptyset" /></a>, or 3) <a href="https://www.codecogs.com/eqnedit.php?latex=n{&space;\succ&space;_{m}}\Psi(m)\,{\text{and}}\,&space;\Psi(n)=\emptyset" target="_blank"><img src="https://latex.codecogs.com/gif.latex?n{&space;\succ&space;_{m}}\Psi(m)\,{\text{and}}\,&space;\Psi(n)=\emptyset" title="n{ \succ _{m}}\Psi(m)\,{\text{and}}\, \Psi(n)=\emptyset" /></a>, or 4) <a href="https://www.codecogs.com/eqnedit.php?latex=\Psi(m)=\emptyset\,{\text{and}}\,&space;\Psi(n)=\emptyset" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Psi(m)=\emptyset\,{\text{and}}\,&space;\Psi(n)=\emptyset" title="\Psi(m)=\emptyset\,{\text{and}}\, \Psi(n)=\emptyset" /></a>.


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## Reference

## License
Copyright (c) [2021] [Yuntao Wang, H. Tom Luan, Zhou Su, Ning Zhang, and Abderrahim Benslimane]

This project is [MIT](https://choosealicense.com/licenses/mit/) licensed. 
