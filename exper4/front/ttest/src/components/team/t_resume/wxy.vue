<script lang="ts" setup>
import { ref, reactive, onMounted } from "vue";
import type { TabsPaneContext } from 'element-plus'

var t_messages = {
        "name" : "王晓英",
        "imageurl" : "team/teacher/wxy.png",
        "qhu_title" : "教授",
        "edu_title" : "清华大学(博士)",
        "email" : "Wxy_cta@qhu.edu.cn",
        "academic_title" : "CCF 会员，ACM 会员，青海省计算机学会常务理事等",
        "main_studying_direction" : "高性能计算，绿色计算等",
        "individual_resume" : ["吉林双辽人，博士，教授，青海大学副校长，曾任计算机技术与应用系常务副主任（2013.6-2019.3）。1999年考入 清华大学计算机科学与技术系计算机科学与技术专业，于 2003 年获得学士学位。2003年9月以免试资格进入清华 大学计算机系攻读博士学位。2008年7月获博士学位，并被评为“清华大学优秀博士毕业生”。2008年8月到青海大 学计算机技术与应用系工作至今。2008年12月进入清华大学博士后流动站从事在职博士后研究工作，2010年12月 完成博士后工作出站。2013年任青海大学计算机系常务副主任。2014.8-2015.2被国家留学基金委选派赴Rutgers , The State University of New Jersey，USA计算机科学系做访问学者。任CCF（中国计算机学会）高级会员、 CCF西宁分部副主席、青海省计算机学会常务理事、中国高等教育学会地方大学教育研究分会监事等社会兼职。",
                                "目前担任《计算机系统平台》《计算机体系结构》课程的主讲工作，作为项目负责人完成国家级项目3项，省科技 厅应用基础研究计划项目2项，校级科研项目2项，横向课题4项，省级教改项目1项，校级一类课程建设项目1项 等；目前作为项目负责人正在承担国家级项目1项，横向课题1项。完成科技成果评价鉴定及成果登记5项，其中 国际领先1项，国际先进3项。主要在数据中心资源管理、数据中心能耗管理与可再生能源利用等方面开展了研究 工作并取得相应成果。2011年获批青海省高校“135高层次人才培养工程”创新教学科研骨干人才，并获“青海省普 通高等学校青年教师小岛奖励金”及“青海省教育系统优秀共产党员”等荣誉称号。2015年被评为“青海省优秀专业 技术人才”及青海省第十批自然科学与工程技术学科带头人。2016年入选青海省“高端创新人才千人计划”拔尖人才 （培养）。2017年获宝钢教育基金“优秀教师奖”。2021年入选青海省“昆仑英才·高端创新人才千人计划”领军人才 （培养），获得首届青海省科学成果奖“青年科技奖状”及省级教学成果奖二等奖。发表研究论文80余篇，获批授权 发明专利9项，软件著作权6项。",
                            ],
        "related_research_situation" : [
            {"name" : "国家自然科学基金项目“融合人工智能技术和数值模式的三江源区中短期降水预测方法研究”（No. 62162053，36万元）；2022.01-2025.12；", "position" : "项目负责人"},
            {"name" : "国家自然科学基金项目“智能电网影响感知的数据中心需求响应策略与机制研究”（No.61762074，39万元）；2018.01-2021.12；", "position" : "项目负责人"},
            {"name" : "国家自然科学基金项目“应用间歇性可再生能源的数据中心资源与能耗管理模型与算法研究”（No.61363019，45万元）；2014.01-2017.12；", "position" : "项目负责人"},
            {"name" : "国家自然科学基金项目“基于虚拟化技术的资源自主管理模型与机制”（60963005，20万元）；2010.1-2012.12,;", "position" : "项目负责人"},
            {"name" : "青海省科技计划项目-应用基础研究计划“GRAPES数值天气预报模式动力框架大规模并行算法与优化技术研究”（No.2019-ZJ-7034，35万元），2019.01-2021.12;", "position" : "项目负责人"},
            {"name" : "清华大学-宁夏银川水联网数字治水联合研究院横向课题（项目编号：SKL-IOW-2020TC2004-01）“基于深度学习和数值模式的短临降水预测系统”，2021.1-2023.1，20万元;", "position" : "项目负责人"},
            {"name" : "清华大学国家重点实验室开放基金 “基于多源卫星的天河工程数据集成平台”（No. sklhse-2017-A-05）, 2017.1-2018.12, 15万元;", "position" : "项目负责人"},
            {"name" : "赛尔网络下一代互联网技术创新项目“基于IPv6的光伏电站监控数据共享平台”(No.NGII20160505)，2017.1-2018.12，5万元;", "position" : "项目负责人"},
            {"name" : "青海省科技计划项目-应用基础研究计划“高压设备热图像在线监测故障诊断策略研究及应用”（No. 2014-ZJ-718），2014.07-2017.07;", "position" : "项目负责人"}
        ],
        "papers" : [
            {"year" : "2022",
             "journal" : ["Chenyu Ma, Jinfang Jia, Zhen Liu, Kun Zhang, Jianqiang Huang, <b>Xiaoying Wang</b>. Simulation of three-dimensional phase field model with LBM method using OpenCL, The Journal of Supercomputing, 2022:78(8), 11092–11110. (SCI源刊，影响因子2.557)",
                        "张琨,贾金芳,严文昕,黄建强,<b>王晓英</b>.GRAPES动力框架中大规模稀疏线性系统并行求解及优化[J/OL].计算机工程: 2022,48(01):149-154+162.（北大核心）",
                        "Zizhen Zhang; Tengfei Cao; <b>Xiaoying Wang</b>; Han Xiao; Jianfeng Guan. VC-PPQ: Privacy-preserving Q-learning Based Video Caching Optimization in Mobile Edge Networks. IEEE Transactions on Network Science and Engineering, 2022年8月3日. (已录用) （SCI源刊，影响因子5.033）",
                        "J. Huang, H. Wang, X. Fei, <b>X. Wang</b> and W. Chen, \" TC-Stream: Large-Scale Graph Triangle Counting on a Single Machine Using GPUs,\" in IEEE Transactions on Parallel and Distributed Systems, vol. 33, no. 11, pp. 3067-3078, 1 Nov. 2022, doi: 10.1109/TPDS.2021.3135329. （SCI源刊，CCF A, 影响因子3.757）",    
                        "曹腾飞，刘延亮，<b>王晓英</b>. 基于改进深度强化学习的边缘计算服务卸载算法, 计算机应用, 2022年7月1日（CSCD源刊，网络首发）",
                        "Yu Zhu, Haixing Zhao *, Jianqiang Huang, <b>Xiaoying Wang</b>. \"Hypernetwork Representation Learning with Common Constraints of the Set and Translation\". Symmetry, 2022（已录用）（SCI源刊，影响因子2.940）",
                        "Yanping Li, Lu Wang, Lei Zhang, Haiwen Chen, Shiying Wang, <b>Xiaoying Wang</b>. HrreNet: semantic segmentation network for moderate and high-resolution satellite images. International Journal of Remote Sensing, 2022: 43(11), pp.4065-4086. （SCI源刊，影响因子3.531）",
                    ],
             "conference" : ["Yu Zhu, Haixing Zhao, Jianqiang Huang, <b>Xiaoying Wang</b>. Hypernetwork Representation Learning with the Transformation Strategy. 2022 6th International Conference on High Performance Compilation, Computing and Communications, 2022, June 23-25.",
                        "Jian Wang, Tengfei Cao, <b>Xiaoying Wang</b>, Man Zhang, Jianfeng Guan. Resource Scheduling in Vehicular Networks with Age of Information and Channel Awareness. IEEE/CIC International Conference on Communications in China. 2022，11–13 August 2022.",
                    ],
            },
            {"year" : "2021",
             "journal" : ["Mengmeng Zhao, <b>Xiaoying Wang*</b>. A Synthetic Approach for Datacenter Power Consumption Regulation towards Specific Targets in Smart Grid Environment. Energies, 2021, 14(9), 2602. (SCI期刊，影响因子3.004, WOS：000650150300001, EI：20212210421500)",
                        "Haodong Bian, Jianqiang Huang*, Lingbin Liu, Dongqiang Huang, <b>Xiaoying Wang</b>. ALBUS: A Method for Efﬁciently Processing SpMV Using SIMD and Load Balancing. Future Generation Computer Systems.Volume 116, March 2021, Pages 371-392. (SCI期刊，影响因子6.125)",
                        "Haodong Bian, Jianqiang Huang, Jiahao Tang, Runting Dong, Li Wu, <b>Xiaoying Wang</b>. PAS: A new powerful and simple quantum computing simulator. Software: Practice and Experience, 2021: 1- 18. (SCI期刊，影响因子2.028)",
                        "Jianqiang Huang, Wentao Han, <b>Xiaoying Wang</b>, Wenguang Chen. Heterogeneous Parallel Algorithm Design and Performance Optimization for WENO on the Sunway TaihuLight Supercomputer. Tsinghua Science and Technology. 2020.25(1): 56-67(SCI源刊，影响因子1.697)",
                        "J. Huang, W. Xue, H. Bian, W. Yan, <b>X. Wang</b> and W. Chen. Helmholtz solving and performance optimization in global/regional assimilation and prediction system. Tsinghua Science and Technology, 2021, 26(3):335-346. (SCI期刊，影响因子1.328)",
                        "张琨,贾金芳,黄建强,<b>王晓英</b>,严文昕. 预处理共轭梯度算法异构并行求解及优化[J/OL].小型微型计算机系统:1-6. 2021-08网络首发（北大核心）",
                        "郭渝洛,边浩东,董润婷,唐嘉豪,<b>王晓英</b>,黄建强.基于SIMD高效并行傅里叶空间图像相似度计算研究[J/OL].计算机工程, 2021,47(11),247-253（北大核心）",
                        "江翠丽,曹腾飞,李长哲,<b>王晓英</b>.基于SVM的视频用户需求预测算法[J].计算机技术与发展,2021,31(05): 38-42.",
                    ],
             "conference" : ["Zhao Mengmeng, <b>Wang Xiaoying*</b>. Datacenter Power Consumption Regulation towards Specific Targets in Smart Grid Environment, 2021 Asia-Pacific Conference on Communications Technology and Computer Science (ACCTCS 2021), 2021, pp.33-36. (EI检索号：20211910328307)",
                            "Dingchang Huang, Runting Dong, <b>Xiaoying Wang*</b>. Modeling and Analysis of Demand Response Strategies for Datacenters in Smart Grid Environment. CONF-CDS 2021: The 2nd International Conference on Computing and Data Science, 2021, No.41, pp.1-6. (EI检索号：20212110387493)",
                            "Wenxin Yan, Jinfang Jia, Kun Zhang, Jianqiang Huang, and Xiaoying Wang. Solving algorithm and parallel optimization of Helmholtz equation in GRAPES model. In The 2nd International Conference on Computing and Data Science (CONF-CDS 2021). Association for Computing Machinery, New York, NY, USA, 2021, Article 171, 1–6. （EI检索号：20212110387319）",
                    ],
            },
            {"year" : "2020",
             "journal" : [" Peicong Luo, <b>Xiaoying Wang*</b> and Yuling Li. The Impact of Datacenter Load Regulation on the Stability of Integrated Power Systems. Sustainable Energy Technologies and Assessments, Volume 42, 2020, 100875. (SCI期刊，影响因子3.427)",
                            "Yuling Li, <b><b><b>Xiaoying Wang</b>*</b></b>, Peicong Luo. Strategies for Datacenters Participating in Demand Response by Two-Stage Decisions. Mathematical Problems in Engineering, 2020, No. 5206082, pp.1-15. (SCI期刊，影响因子，1.009，WOS检索号：000559318400009， EI检索号：20203309052346)",
                            "Jianqiang Huang, Wentao Han, <b>Xiaoying Wang</b>, Wenguang Chen. Heterogeneous Parallel Algorithm Design and Performance Optimization for WENO on the Sunway TaihuLight Supercomputer, TSINGHUA SCIENCE AND TECHNOLOGY, 2020, 25(1):56-67. (SCI源刊)",
                            "Jianqiang Huang, Wei Qin, <b>Xiaoying Wang</b>, Wenguang Chen. Survey of external memory large‑scale graph processing on a multi‑core system. The Journal of Supercomputing, 2020, 76(1): 549-579. (SCI源刊)",
                            ],
             "conference" : ["Zhao Mengmeng, <b><b>Xiaoying Wang</b>*</b> . A Survey of Research on Datacenters Using Energy Storage Devices to Participate in Smart Grid Demand Response. 2020 IEEE International Conference on Power, Intelligent Computing and Systems (ICPICS 2020), Jul. 2020, Shenyang, China, pp.22-26. (EI检索号：20204309377975)",
                                "Peicong Luo, <b><b>Xiaoying Wang</b>*</b>. Dynamic Power Management Strategies for Datacenters towards Maintaining Grid Stability. 2020 4th High Performance Computing and Cluster Technologies Conference (HPCCT 2020), Jul. 2020, Qingdao, China, pp.261-266. (EI检索号：20203809193237)",
                                "Yuling Li, <b><b>Xiaoying Wang</b>*</b>, Peicong Luo, Dingchang Huang, Mengmeng Zhao. A Two-stage Demand Response Strategy for Datacenters in the Smart Grid Environment. 2020 the 3rd International Conference on Energy, Electrical and Power Engineering (CEEPE 2020), Apr. 2020, Chongqing, China. Journal of Physics: Conference Series (JPCS), vol. 1585, No. 012025. (EI检索号：20203209023041)",
                                "Dingchang Huang, Xuejiao Yang, <b><b>Xiaoying Wang</b>*</b>. Location and cost optimization of datacenters and solar power plants. 2020 4th International Conference on Computer Science and Artificial Intelligence (CSAI 2020)."]
            },
            {
                "year":"2019",
                "journal":["Peicong Luo, <b><b>Xiaoying Wang</b>*</b>, Hailong Jin, Yuling Li and Xuejiao Yang. Smart-Grid-Aware Load Regulation of Multiple Datacenters towards the Variable Generation of Renewable Energy. Applied Sciences, 2019, 9(3): 518. (SCI源刊，影响因子2.217, WOS入藏号：000459976200158)",
                            "Yuling Li, <b><b>Xiaoying Wang</b>*</b>, Peicong Luo and Qingyi Pan. Thermal-Aware Hybrid Workload Management in a Green Datacenter towards Renewable Energy Utilization. Energies 2019, 12(8), 1494. (SCI源刊，影响因子2.707, EI检索号：20192006919570, WOS入藏号：000467762600087)"],
                "conference": ["Yuling Li, <b><b>Xiaoying Wang</b>*</b>, Peicong Luo and Xuejiao Yang. Temperature-aware Workload Management for Sustainable Datacenters Powered by Renewable Energy. 2019 the 3rd International Conference on High Performance Compilation, Computing and Communications (HP3C-2019), 2019, pp.149-154. (EI检索号：20191706811608, ISTP检索号：000473329300027)",
                                "Jiangwei Sheng, <b><b>Xiaoying Wang</b>*</b>, Tengfei Cao, Xiaodan Zhang. Study on Different Parameterization Schemes to Simulate the Physical Process of a Heavy Rainfall on Qinghai-Tibet Plateau. Advance Management Science. 2019 International Conference on Energy, Power, Environment and Computer Application (ICEPECA2019), 2019, pp.145-150. (ISTP检索号: 000471628600025）",
                                "Guojing Zhang, <b><b>Xiaoying Wang</b>*</b>, and Yuling Li. Implementation and Improvement of Solar Power Data Monitoring and Sharing Platform based on IPv6. The 9th International Workshop on Computer Science and Engineering (WCSE 2019), June 2019, pp.704-709."]
            },
            {
                "year":"2018",
                "journal":["Qingyi Pan, <b><b>Xiaoying Wang</b>*</b>. Independent travel recommendation algorithm based on analytical hierarchy process and simulated annealing for professional tourist. Applied Intelligence, 2018, 48(6): 1565-1581. (SCI源刊，影响因子1.904， EI检索号：20173504093147）",
                            " PeiCong Luo, <b><b>Xiaoying Wang</b>*</b>. Research on the Resource Allocation Algorithm based on Forecasting in Mobile Cloud Computing. Journal of Intelligent &amp; Fuzzy Systems, 2018, 35(2):1315-1324. (SCI源刊，影响因子1.426, WOS入藏号：000450368900001，EI检索号: 20183805831689)"],
                "conference":["Peicong Luo, <b><b>Xiaoying Wang</b>*</b>, Hailong Jin, Xuejiao Yang and Yuling Li. Load Management for Multiple Datacenters towards Demand Response in the Smart Grid Integrating Renewable Energy. 2018 2nd International Conference on Computer Science and Artificial Intelligence (CSAI 2018), Dec. 2018, pp.140-144.（EI检索号：20191106628980, ISTP检索号：000469786300027）",
                                "Guojing Zhang，<b>Xiaoying Wang</b>，Jie Li，Xuejiao Yang. Design and Implementation of the Data Sharing Platform of a Photovoltaic Power Station over IPv6. 2018 5th International Conference on Mechatronics Engineering and Computer Sciences (ICMECS 2018), 2018, pp: 1193-1197.",
                                "Xuejiao Yang, <b><b>Xiaoying Wang</b>*</b>, Hailong Jin, Yuling Li and Peicong Luo. Research on Location and Capacity Planning of Datacenters in Smart Grids with Renewable Sources. 2018 International Conference on Computer, Communications and Mechatronics Engineering (CCME 2018), Dec. 2018, pp. 201-209. （ISTP检索号：000473811700037）",
                                "Xuejiao Yang, <b><b>Xiaoying Wang</b>*</b>, Jiangwei Sheng, Yuling Li, Peicong Luo. Parallelization and Performance Optimization of the Jacobi Stencil Algorithm. 2018 International Conference on Sensing, Diagnostics, Prognostics, and Control, 2018, pp: 719-723. (EI检索号：20191506770084，ISTP检索号：000469086600130)"]
            },
            {
                "year":"2017",
                "journal":["Peng Cui, <b><b>Xiaoying Wang</b>*</b>. Modeling the Decision Process of Optimal Travel Route based on Analytic Hierarchy Process. Internet Journal of Grid and Distributed Computing. (ISSN: 2005-4262), 2017, 10(2): 21-36. (ESCI收录，WOS检索号: 000401474700003)",
                            "Guojing Zhang, <b><b>Xiaoying Wang</b>*</b>, Mengqin Yang. Managing and Scheduling Approximate Applications to Utilize Renewable Energy in Cloud Computing Datacenters. APPLIED ECOLOGY AND ENVIRONMENTAL RESEARCH, 2017, 15(3):307-321. (SCI源刊，影响因子：0.681，WOS检索号：000403811200022) ● ISSN 1589 1623 (Print)"],
                "conference":["Fengyu Guo, <b><b>Xiaoying Wang</b>*</b>. Research on Energy Consumption Modeling Method for Multi-Type Hybrid Applications. 2017 International Conference on Applied, Mathematics, Modelling and Statistics Application (AMMSA 2017), Advances in Intelligent Systems Research (AISR), 2017, vol. 141, pp.14-20. (ISTP检索号: 000416087700004)",
                                "张国晶，<b>王晓英</b>，杨雪娇. 面向太阳能利用的云数据中心资源调度算法研究. 2017全国高性能学术年会(HPCChina2017), 2017, pp.500-505.",
                                "杨雪娇，<b>王晓英</b>，盛江玮. Jacobi Stencil算法的并行化实现及性能优化研究. 2017全国高性能学术年会(HPCChina2017), 2017, pp.594-595.",
                                "盛江玮，<b>王晓英</b>，曹腾飞，张小丹. WRF模式中物理过程参数化方案对青藏高原一次强降水模拟的影响研究. 2017全国高性能学术年会(HPCChina2017), 2017,pp.590-591."],
            },
            {
                "year":"2016",
                "journal":["Qingyi Pan, <b><b>Xiaoying Wang</b>*</b>. Performance Evaluation and Optimization of HPCG benchmark on CPU + MIC platform. International Journal of Hybrid Information Technology, 2016, 9(11): 239-254. (EI 检索号: 20165103134003)"],
                "conference":["<b>Xiaoying Wang</b>, Kunchang Li, Guojing Zhang, Lei Zhang. Modeling the Power Consumption of Multiple Typical Applications based on Linux. Proceedings of the 2016 International Conference on Communications, Information, Management and Network Security (CIMNS2016), 2016. Advances in Computer Science Research (ISSN: 2352-538x), 2016, pp.43-46. (WOS检索号：000390854400011)",
                                "<b>Wang Xiaoying</b>, Yi Zhengming, Liu Xiaojing, Cao Tengfei. Establishing the Platform of Operating System Experiments for Application-oriented Talent Cultivation. 2016 3rd International Conference on Economic, Business Management and Education Innovation (EBMEI 2016), May 2016, Lecture Notes in Management Science, vol. 56, pp. 310-315. (WOS检索号：000391644000054)",
                                "MENG Qiao, <b>WANG Xiaoying</b>, ZHANG Yu_an. Research on a Least Squares Thresholding Algorithm for Pavement Crack Detection. 6th International Conference on Information Science and Technology, May 2016, Dalian, China, pp. 465-469. (EI检索号: 20162902609667)",
                                " Huang, Jianqiang, Wu, Huan; <br>Wang, Xiaoying</br> and Yi, Zhengming. Research and application of online monitoring fault diagnosis for infrared image and visible image registration. 2016 6th International Workshop on Computer Science and Engineering (WCSE 2016), Tokyo, Japan, 2016, pp. 765-772. (EI检索号：20163202697445)"]
            },
            {
                "year":"2015",
                "journal":["<b>Xiaoying Wang</b>; Zhihui Du; Yinong Chen; Mengqin Yang. A Green-aware Virtual Machine Migration Strategy for Sustainable Datacenter Powered by Renewable Energy. Simulation Modelling Practice and Theory, 2015, vol.58, Part1, pp. 3-14. (SCI期刊，ISSN:1569-190X, 影响因子：1.383，WOS: 000363273400002，IDS 号: CU1IF) （EI检索号：20150600502786）",
                            "Guojing Zhang, <b><b>Xiaoying Wang</b>*</b>, Zhihui Du. Research on the Prediction of Solar Energy Generation based on Measured Environmental Data. International Journal of u- and e- Service, Science and Technology. 2015: 8(5): 385-402. （EI检索号：20152600975359）",
                            "解辉，<b>王晓英</b>，金鑫. 数据中心间歇性绿色能源供给管理策略研究. 微型机与应用， 2015， 34(18): 69-72.",
                            "解辉，<b>王晓英</b>，金鑫. 基于模板知识的带噪音半结构文本数据自动分词方法研究. 微型机与应用，2015，34(17)：89-95.",
                            "解辉，<b>王晓英</b>，金鑫.数据中心间歇性绿色能源功率变化模型设计, 2015, 34(16): 11-14."],
                "conference":["Guojing Zhang, <b><b>Xiaoying Wang</b>*</b>, Zhihui Du. Review of Heterogeneous Computing based on GPU. 2015 International Conference on Informatics, Control and Automation (ICA2015), July, 2015, Phuket, Thailand, pp.175-180. （ISTP检索号：000377614100032）",
                                "<b>Xiaoying Wang</b>, Divya Kurthakoti Chandrashekhara, Md Haque, Inigo Goiri, Ricardo Bianchini, Thu Nguyen. Grid-Aware Placement of Datacenters and Wind Farms. IGSC 2015 : 2015 Sixth International Green and Sustainable Computing Conference, Dec 2015, Las Vegas, Nevada, USA, pp. 1-8. (EI检索号：20161602256021) ISTP检索号：000380428700031",
                                "<b>Xiaoying Wang</b>, Yu-an Zhang, Xiaojing Liu, Tengfei Cao. Exploiting the potential of data centers in the smart grid. International Conference on Intelligent Manufacturing and Computational Technology (IMCT2015)，Nanjing, China, 2015, pp. 403-409. (ISTP检索号：000385239300057)",
                                "<b>王晓英</b>，沈茜，孟永伟，李东. 数据中心与风电厂在电网中的部署及交互建模仿真研究. 全国高性能计算学术年会， CCF HPC China 2015, pp. 721-722."]
            }
        ],
        "technological_achievements" : [
            "成果名称： 智能电网影响感知的数据中心需求响应策略与机制研究<br/><br/>批准登记号： 9632022J0263 推荐单位： 青海大学<br/>完成单位 青海大学<br/>完成人： 王晓英、黄建强、曹腾飞、贾金芳、张国晶、解辉、张玉安、张小丹、杨培、任洋甫、薛万东<br/>成果公报内容： 本项目以接入可再生能源的智能电网环境中部署和运行的数据中心为研究对象，面向可再生能源随季节和天气而随时变化的特性及电网自身负载的变化特性，考虑电网运行效率和安全性问题的约束，对能够感知电网运行状态的数据中心需求响应的策略和关键机制进行研究，旨在设计全面、完整的研究体系结构，并提供解决其中一些关键问题的思路。研究成果能够为绿色数据中心中可再生能源的利用和研究提供重要的参考，有助于进一步提高数据中心服务提供者的总体收益，也可促进可再生能源应用的快速发展和更大规模并网，对节能减排及环境保护具有重要的意义。成果达到国际领先水平。<br/>",
            "成果名称： GRAPES数值天气预报模式动力框架大规模并行算法与优化技术研究</br></br>批准登记号： 9632022J0272 推荐单位： 青海大学</br>完成人： 王晓英、贾金芳、黄建强、吴利、张国晶、张琨、严文昕、边浩东</br>成果公报内容： 中国气象局的“十四五”数值预报发展规划指出，到 2025年，面向天气气候一体化数值预报业务发展和气象服务保障需求，建成技术自主可控，长、 中、短期有机衔接的数值预报业务体系，探索发展天气气候一体化的地球系统数值预报，构建统筹集约、协同发展的数值预报研发体制机制，有效支撑气象事业高质量发展和气象强国建设。本项目选取对GRAPES动力框架中的热点函数赫姆霍兹方程求解进行性能优化研究，为GRAPES模式快速高效运行、研究及应用提供有效技术参考，同时高效的预报也能在很大程度上避免灾害损失。成果达到国际先进水平。</br>",
            "成果名称： 应用间歇性可再生能源的数据中心资源与能耗管理模型与算法</br></br>批准登记号： 9632019J0237</br>推荐单位： 青海大学</br>完成单位: 青海大学</br>完成人： 王晓英、黄建强、解辉、张玉安、张国晶、张小丹、刘志强、刘晓静、樊丽华、都志辉、回新宁</br>成果公报内容： 本成果以国家自然科学基金项目为背景，针对应用间歇性可再生能源的数据中心资源与能耗管理模型与算法展开研究，从模型、策略、算法及系统入手，对数据中心混合类型应用进行了性能建模和功耗建模，提出了资源管理和任务调度的策略和算法。对可再生能源利用及管理策略进行了研究，针对可近似的应用，提出面向可再生能源利用的自适应调度算法，有效提高了对可再生能源的利用率。通过潮流计算仿真的方法对数据中心和风力发电厂在接入电网之后的影响进行了研究，提出了一种数据中心接入电网的建设总成本优化方法。项目在混合应用和可近似应用功耗建模、可再生能源利用自适应调度算法和数据中心电力成本优化研究方面具有一定创新性。研究成果能够为未来绿色数据中心的构建、设计和管理提供重要的参考和技术支撑，也能够为解决可再生能源并网限制问题提供新的途径，从而促进可再生能源的大力开发和使用。成果达到国际先进水平。</br>",
            "成果登记：“基于虚拟化技术的资源自主管理模型与机制”</br></br>登记号：9632014J0128</br>评价单位：青海省科技厅</br>评价日期：2014.01.16</br>完成单位：青海大学</br>主要研究人员：王晓英、解辉、薛媛媛、樊丽华、刘晓静、王瑞、李鑫丽、金鑫、贾续涵、都志辉、刘文杰、张天乐、何禹、胡敬坤、高涛</br>成果公报内容：本课题以国家自然科学基金项目为背景，对虚拟资源的自主管理模型与机制进行了研究：设计和构建了云仿真中心系统；提出了一种典型虚拟机映像机制TVA；对应用性能建模和QoS估测方法进行了研究，提出了一种基于无显式建模的方法进行QoS估测；提出多种类型异构资源的协同分配模型；对资源预约管理进行了研究，提出了自适应的混合任务管理方法；设计和实现了云监控架构SCMF；设计了基于自主计算思想的QoS管理架构与方法。本课题对资源管理过程中所涉及到的监控、建模、估测、分析和优化配置等各个环节均进行了研究，并将不同环节的研究方法和结果进行了有机整合，使得整个自适应资源自主管理的过程能够有利于用户满意度的提高及系统效益的最大化，成果达到国内领先水平。</br>",
            "成果登记：高压设备热图像在线监测故障诊断策略研究及应用</br></br>登记号：9632018J0163          推荐单位：青海大学</br>课题来源：地方计划          评价单位：青海省科技厅</br>　　研究起止时间：2014.07至2017.07      评价日期：2017.11.10</br>　　完成单位：青海大学</br>主要研究人员：王晓英、黄建强、张玉安、王瑞、曹腾飞、刘晓静、张国晶</br>成果公报内容：本课题以青海省科技厅应用基础研究项目为背景，建立红外图像温度场分布模型，建立必要的红外图像库，建立了红外热图像故障诊断原型系统,该系统能够自动循环采集变电站电气设备的红外图像,通过提取目标设备的温度信息进行故障判别。为了解决机械传动造成的图像位置偏差导致系统难以对感兴趣设备进行定位监测的问题,提出了基于干线对的匹配方法实现红外图像与可见光图像的多源图像匹配算法，将故障区域在可见光图像上标注出来。本课题对红外热图像和可见光图像配准中所涉及到的算法、建模、和调优等各个环节均进行了研究，并将不同环节的研究方法和结果进行了有机整合，使得整个过程能够有利于用户满意度的提高及系统效益的最大化。成果达到国内领先水平。</br>"
        ],
        "achievements_list" : [
            "专利授权：授权日期：2022年8月9日，名称：智能电网环境中数据中心功耗调节方法、系统、介质及设备，赵梦梦;王晓英。（公开(公告)号:CN112994037A 公开(公告)日:2021.06.18，申请号:CN202110141041.2，申请日:2021.02.02。 证书编号5373438。",
            "专利授权：授权日期2022年7月19日，授权公告号：CN111461920B, 专利号ZL202010209948.3。申请日期：2020年3月23日，一种面向智能电网的数据中心需求响应方法和系统。李玉玲、王晓英，申请号：CN202010209948.3。公开号：CN111461920A",
            "专利授权，授权日期2022年7月19日，授权公告号CN109888817B，专利号ZL201811562978.1。申请日期：2018年12月20日，申请号：201811562978.1，名称：对光伏电站和数据中心进行位置部署和容量规划方法。杨雪娇、王晓英，公开号：CN109888817A.",
            "专利授权：授权日期2022年4月29日，授权公告号：CN112488447B，申请日期：2020年11月2日，一种基于需求响应合同的数据中心的功耗调控方法及系统，专利号：ZL 202011205373.4 申请日:2020.11.02。董润婷;王晓英。证书编号：5121950",
            "专利授权：授权日期2022年4月29日，授权公告号：CN111628497B，申请日期：2020年5月22日，一种面向电网稳定性的动态负载管理方法及计算机设备。罗佩聪、王晓英，专利号：ZL 202010442923.8，证书编号：5119888",
            "专利授权：授权日期2021年7月27日，授权公告号：CN108052387B，申请日期：2017年11月15日，申请号：201711131885.9，名称：一种移动云计算中的资源分配预测方法及系统。罗佩聪、王晓英。公开号：CN108052387A 专利号：ZL 201711131885.9",
            "专利授权：授权日期：2021年7月13日，名称：一种可再生能源数据中心管理方法及装置。李玉玲、王晓英。授权公告号：CN110008515B，专利号：ZL 2019 1 0171263.1。申请日期：2019年3月7日，申请号：201910171263.1，公开号：CN110008515A。",
            "专利授权：授权日期：2019年10月29日，授权公告号：CN106886274B。专利号：ZL 2017 1 0053681.1。名称：一种数据中心能耗的管理方法及装置，王晓英、杨梦琴、张国晶。2017.7.5。公开号：CN106886274A 申请日期：2017年01月22日，申请号201710053681.1，",
            "专利授权：授权日期：2020年10月9日，授权公告号：CN109638837B。专利号：ZL 2018 1 1639180.2。名称：一种面向新能源并网的动态负载管理方法及系统。罗佩聪、王晓英，公开号：CN109638837A。请日期：2018年12月29日，申请号：201811639180.2。",
            "软件著作权：2017年6月30日，基于IPv6的光伏电站监控数据共享平台V1.0，登记号：2018SR375159",
            "软件著作权：2018年3月30日，基于Hadoop的多源异构数据实时自动存储软件V2.0，登记号：2018SR777474 软件著作权：2019年5月21日，基于IPv6的光伏电站监控数据共享平台V2.0，登记号：2019SR0494346"
        ]
    }

t_messages.imageurl = require("../../../assets/" + t_messages.imageurl)

const activeName = ref("first")
const handleSelect = () => {

}
onMounted(() => {

})
const handleClick = (tab: TabsPaneContext, event: Event) => {
  console.log(tab, event)
}
</script>

<template>
<br/>
<el-row>
    <el-col :span="4"></el-col>
    <el-col :span="16">
        <el-card>
            <!-- 上半部分 -->
            <el-row>
                <el-col :span="2"></el-col>
                <!-- 左边为基础信息 -->
                <el-col :span="6">
                    <el-avatar :size="168" :src="t_messages.imageurl" fit="fill" class="el_image" />
                    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                        <el-tab-pane class="el_name" label="姓名" name="first">{{t_messages.name}}({{t_messages.qhu_title}})</el-tab-pane>
                    </el-tabs>
                    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                        <el-tab-pane class="el_edu_title" label="学历" name="first">{{t_messages.edu_title}}</el-tab-pane>
                    </el-tabs>
                    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                        <el-tab-pane class="el_title" label="学术职称" name="first">{{t_messages.academic_title}}</el-tab-pane>
                    </el-tabs>
                    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                        <el-tab-pane class="el_main_studying" label="主要研究方向" name="first">{{t_messages.main_studying_direction}}</el-tab-pane>
                    </el-tabs>
                    <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
                        <el-tab-pane class="el_email" label="联系方式" name="first">{{t_messages.email}}</el-tab-pane>
                    </el-tabs>
                </el-col>
                <el-col :span="2"></el-col>
                <!-- 右边为个人简历 -->
                <el-col :span="12">
                    <el-tabs type="card" class="demo-tabs">
                        <el-tab-pane>
                        <template #label>
                            <span class="custom-tabs-label">
                            <el-icon><calendar /></el-icon>
                            <span>个人简介</span>
                            </span>
                        </template>
                        <p v-for="i_resume in t_messages.individual_resume" :key="i_resume" style="text-indent: 2em;">{{i_resume}}</p>
                        </el-tab-pane>
                    </el-tabs>
                </el-col>
                <el-col :span="2"></el-col>
            </el-row>
            <!-- 下半部分 -->
            <br/>
            <el-row>
                <el-col :span="2"></el-col>
                <el-col :span="20">
                    <!-- 主持、参与科研情况 -->
                    <el-tabs type="border-card" class="demo-tabs">
                        <el-tab-pane>
                        <template #label>
                            <span class="custom-tabs-label">
                            <el-icon><calendar /></el-icon>
                            <span>主持/参与科研情况</span>
                            </span>
                        </template>
                        <p v-for="(rrs,index) in t_messages.related_research_situation" :key="rrs" style="margin: 5px;">
                            [{{index+1}}]{{rrs.name}}<b>{{rrs.position}}</b>
                        </p>
                        <!-- <el-card v-for="(rrs,index) in t_messages.related_research_situation" :key="rrs" style="margin: 5px;">
                            [{{index}}]{{rrs.name}}<b>{{rrs.position}}</b>
                        </el-card> -->
                        </el-tab-pane>
                    </el-tabs>
                    <br/>
                    <!-- 学术论文发表 -->
                    <el-tabs type="border-card" class="demo-tabs">
                        <el-tab-pane>
                        <template #label>
                            <span class="custom-tabs-label">
                            <el-icon><calendar /></el-icon>
                            <span>学术论文发表</span>
                            </span>
                        </template>
                        <el-tabs tab-position="left" type="border-card" class="demo-tabs">
                            <el-tab-pane v-for="rrs in t_messages.papers" :label="rrs.year" :key="rrs">
                                <el-tabs type="card">
                                    <el-tab-pane label="期刊论文">
                                        <span v-for="(j,index) in rrs.journal" :key="j">[{{index+1}}]<p style="display: inline;" v-html="j"></p><br/><br/></span>
                                    </el-tab-pane>
                                </el-tabs>
                                <el-tabs type="card">
                                    <el-tab-pane label="会议论文">
                                        <span v-for="(c,index) in rrs.conference" :key="c">[{{index+1}}]<p style="display: inline;" v-html="c"></p><br/><br/></span>
                                    </el-tab-pane>
                                </el-tabs>
                            </el-tab-pane>
                        </el-tabs>
                        </el-tab-pane>
                    </el-tabs>
                    <br/>
                    <!-- 科技成果登记 -->
                    <el-tabs type="border-card" class="demo-tabs">
                        <el-tab-pane>
                        <template #label>
                            <span class="custom-tabs-label">
                            <el-icon><calendar /></el-icon>
                            <span>科技成果登记</span>
                            </span>
                        </template>
                        <span v-for="(ta,index) in t_messages.technological_achievements" :key="ta">
                            [{{index+1}}]<p style="display: inline;" v-html="ta"></p><br/><br/>
                        </span>
                        </el-tab-pane>
                    </el-tabs>
                    <!-- 业绩列表 -->
                    <el-tabs type="border-card" class="demo-tabs">
                        <el-tab-pane>
                        <template #label>
                            <span class="custom-tabs-label">
                            <el-icon><calendar /></el-icon>
                            <span>业绩列表（近5年）</span>
                            </span>
                        </template>
                        <span v-for="(al,index) in t_messages.achievements_list" :key="al">
                            [{{index+1}}]<p style="display: inline;" v-html="al"></p><br/><br/>
                        </span>
                        </el-tab-pane>
                    </el-tabs>
                </el-col>
                <el-col :span="2"></el-col>
            </el-row>
        </el-card>
    </el-col>
    <el-col :span="4"></el-col>
</el-row>
</template>

<style scoped>
.el_image{
    height: 210px;
    width: 170px;
}
.el_name{
    font-weight: bold;
    font-size: 18px;
}
.el_edu_title{
    font-weight:lighter;
    font-size: 16px;
}
.el_title{
    font-weight:lighter;
    font-size: 16px;
}
.el_main_studying{
    font-weight:lighter;
    font-size: 16px;
}
.el_email{
    font-style:italic;
    font-weight: bold;
    font-size: 14px;
}
</style>

