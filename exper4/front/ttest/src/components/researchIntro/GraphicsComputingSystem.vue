<template>
    <div class="tz-gallery">
					
                    <b>方向介绍：</b>	
                    <p style="font-size:0.9rem;">
                        <br>
                            &nbsp;&nbsp;&nbsp;&nbsp;图是一种重要的数据结构，它能充分表达自然界中事物的联系和依赖属性，所以在计算机领域中广泛应用。很多问题能在图论 支撑下借助图相关的算法得到高效解决，例如图形着色，网络路由，网络流等。 但是，近年来随着Web2.0、大数据、社交网络、机器学习和数据挖掘（MLDM - MachineLearningand Data Mining）等技术的高速发展，很多领域抽象出来的图规模呈指数级增长。 图中边的数量可达到亿万级别，另外再加上自然图往往表现出非常倾斜的幂律分布power-law特性，对图计算带来了巨大挑战。
                            <br>
                            </p><div align="center">
                                <a class="lightbox">
                                    <img class="research-sm-img" height="280" width="400" src="../../assets/researchIntro/chatu_tujisuan.jpg" alt="Coast">
                                </a>
                            </div>
                            <br>
                            &nbsp;&nbsp;&nbsp;&nbsp;研究图计算高效处理大规模图数据，能推动社交网络分析、语义web分析、生物信息网络分析、自然语言处理和MLDM等新兴应用领域的发展。 此外图计算的应用领域还包括：流量图，用来监控和应对道路事故，分析网络安全，网页搜索；生物图，进行研究药物模型（例如蛋白质相互作用），预测疾病爆发；社交图，对舆情分析， 推荐人或产品和信息流跟踪等。
                            <br>
                            <br>
                            &nbsp;&nbsp;&nbsp;&nbsp;现有的图处理系统可以通过是否是单机还是集群、是否运行在内存还是磁盘与内存交换，可以将图处理系统分为单机内存图处理系统、 单机核外图处理系统、分布式内存图处理系统、分布式核外图处理系统。单机内存图处理系统就是图处理系统运行在单机环境，并且将图数据全部缓冲到内存当中。 单机核外图处理系统就是图处理系统运行在单机环境，并且通过计算将图数据通过不断的与内存和磁盘进行交互进行高效的图算法。 分布式内存系统就是图处理系统运行在分布式集群环境，并且所有的图数据加载到内存当中。分布式核外图计算系统将Single-machine out-of-core systems拓展为集群， 能够处理边数量级为trillion的图。
                            <br>
                            <br>
                            &nbsp;&nbsp;&nbsp;&nbsp;图算法可以分为以遍历为中心的算法和以计算为中心的算法。以遍历为中心的算法有：BFS、DFS、SSSP、Prim、Dijkstra、 MST、SPFA、Bellman Ford、Floyd Warshall 等；以计算为中心的算法有：PageRank、MIS、Connected Component、Graph Color、Triangle Count、Random Work、Subgraph Matching 等。
                    
                    <p></p>
                    
                            </div>
</template>