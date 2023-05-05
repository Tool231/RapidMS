# RapidMS
We conducted a comparative experiment involving four participants: one expert with substantial practical and theoretical experience in microservices architecture, who performed manual partitioning and microservice modeling from the requirements model, and four experimenters with extensive software development experience but limited knowledge of microservices architecture, three of the used our tools to assist in microservices design and the last one identify the microservices manully. All participants decomposed the requirements models for four cases within the same timeframe, ultimately producing the final generated microservices models. Quality of these microservices models was quantified, as illustrated:
![image](https://user-images.githubusercontent.com/132594916/236363381-88c956f3-4a54-4eee-b018-d62d01ddbc69.png)
**IFN**: Average number of interfaces per microservice(IFN) is described as the average number of interfaces in the system, the smaller the value, the better.In our problem, IFN represents the number of interfaces between microservices and ignores the interfaces provided by the microservice to the user.  

$$
IFN=\frac{1}{N} \sum_{i=1}^{N} |Interface _{i}|
$$

**Instability**: Instability is defined as the ratio of the number of interfaces provided by a microservice to the sum of the number of interfaces it provides and the number of interfaces required. The higher Instability is, the more stable the microservice will be.

$$
Instability=\frac{\left|ProvideInterface\right|}{\left|ProvideInterface\right|+\left|RequiredInterface\right|}
$$

**CHD**: Cohesion at domain level(CHD) measures the cohesiveness of interfaces provided by a service at the domain level. The higher the CHD, the more domain cohesive this service is.

$$
CHD= \frac{1}{N^2}\sum_{K=1}^{N}\sum_{M=1}^{N}\frac{\left|f_{\text {term }}\left(o p r_{k}\right) \cap f_{\text {term }}\left(o p r_{m}\right)\right|}{\left|f_{\text {term }}\left(o p r_{k}\right) \cup f_{\text {term }}\left(o p r_{m}\right)\right|}
$$

**CMQ**: Conceptual Modularity Quality(CMQ) draws on the metrics of article, which can be used in our approach to evaluate domain model decomposition results well. It is defined as the difference between the average degree of relatedness of the domain model within a microservice and the average degree of relatedness of the domain model between microservices.

**UCM**: For two scenarios (use cases), comprehensively calculate their correlation degree from three aspects: user correlation, scenario correlation correlation, and domain concept correlation. 

Actor correlation: User correlation is defined as the dependency between a use case caused by the same user associated with them. In a use case diagram, the relationship between the actor and use cases reflects the interaction between the use cases and the system. Different entities connected to the same actor provide services for the same actor, the similarity between them is defined as, and the set of defined and connected is.
$$
Corr_A(UC_a,UC_b)=\left\{
\begin{aligned}
0, Actor(UC_a) \cap Actor(UC_b) = \varnothing \\
1, Actor(UC_a) \cap Actor(UC_b) \neq \varnothing  \\
\end{aligned}
\right.
$$

Function correlation: An Include or Extend relationship between the use cases proves that there is a use-and-be used the relationship between the two associated use cases. As a preliminary solution, the use cases at both ends of the \textit{Include} and Extend are defined as strongly correlated associations. We define $Corr_F$($UC_a$, $UC_b$) to indicate the relevance of the association relationship between use cases. Returns a Bool value indicating whether it is related to having an Include or Extend association.
<img width="643" alt="image" src="https://user-images.githubusercontent.com/132594916/236365921-6fa3001d-bad3-4580-8359-7a7a39835ffe.png">



Domain correlation: The relevance of the use domain correlation($Corr_D$($UC_a$, $UC_b$))is between [0,1], and the higher the value, the higher the domain relevance between the use cases. Let the number of use cases of the system be N, and take $V_{x}$ to be a vector of dimension N. V[i] = 1 means $V_{x}$ uses the $Entity_i$. The domain correlation between use cases $UC_x$ and $UC_y$ is defined as the cosine of the $V_{x}$ and $V_{y}$.

<img width="641" alt="image" src="https://user-images.githubusercontent.com/132594916/236365945-055705aa-7c51-4f12-9cd1-312406177ec5.png">



Let the number of use cases be $N_{UC}$. Then, the correlation matrix M with dimension $N_{UC}$*$N_{UC}$ is obtained according to the three correlations. The element $m_{ij}$ in the i-th row and j-th column of the matrix represents the correlation of the $UseCase_i$ and $UseCase_j$,  which is calculated by adding the three correlations as follows. 

$$
m_{i j}=0.2* Corr_{A}(U C_{i}, U C_{j})+0.3* Corr_{Ass}(U C_{i}, U C_{j})\\+0.5
* Corr_{E}(U C_{i}, U C_{j})
$$
