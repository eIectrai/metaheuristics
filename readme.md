# Metaheuristics
RESOURCES:

Intel i7 8-core 1.80GHz (although multicore was not leveraged in this project)

Python 3.8 with Virtualenv

Jupyter Notebook

Scipy for CEC (used for its simplicity even though it offers only few options for global optimization and moderate parallellization capacity compared to other libraries such as Pygmo)

Scikit-opt for TSP (still in development but handy with several algorithm options adapted to TSP)

---
[F1 SHIFTED SPHERE](https://github.com/eIectrai/metaheuristics/tree/master/F1_Shifted_Sphere) (with Differential Evolution):

Problem has D local minima including a global one. I tried a 'brute' approach by setting a big population size to get good-enough candidates, then individuals follow the leader with best1bin strategy and high crossover. Mutation rate is based on the following recommendation: https://en.wikipedia.org/wiki/Differential_evolution#/media/File:DE_Meta-Fitness_Landscape_(Sphere_and_Rosenbrock).JPG. Got help for dimension 500 with final local search to make sure the global minimum is reached.

---
[F2 SHIFTED SCHWEFEL](https://github.com/eIectrai/metaheuristics/tree/master/F2_Shifted_Schwefel) (with Basin Hopping): 

Problem was too long to converge with Differential Evolution at dimension 500 because of slow slopes close to minima; a self-adaptative version of Differential Evolution could work better but isn't included in Scipy. So I used Basin Hopping instead and opted for BFGS as the local search algorithm after each hop. Had to hop 10 times to find the global minimum. Slightly increased the temperature and stepsize compared to default values.

---
[F3 SHIFTED ROSENBROCK](https://github.com/eIectrai/metaheuristics/tree/master/F3_Shifted_Rosenbrock) (with Simulated Annealing):

Again, trying to use Differential Evolution on Rosenbrock proved to be challenging because problem has high cliffs and very long valleys. So I went for another mixed-method based on Simulated Annealing with complementary local search. The main parameter to be found is the number of global search iterations needed to get low enough in the valley (200 for dimension 50, 700 for dimension 500) so that local search can finish the job.

---
[F4 SHIFTED RASTRIGIN](https://github.com/eIectrai/metaheuristics/tree/master/F4_Shifted_Rastrigin) (with Differential Evolution):

Scipy sets population as an integer-multiple of dimension so, for dimension 500, population is still big while studies proved efficiency of populations in the 50-100 range. Problem has overall convexity but many local optima, so we still adopt a best1exp strategy but individuals behave more independently and explore local surroundings based on a reduced crossover and dithering mutation rate. Global minimum is long to reach at dimension 500 even though Scipy's Differential Evolution implementation lets us set up multiple workers.

---
[F5 SHIFTED GRIEWANK](https://github.com/eIectrai/metaheuristics/tree/master/F5_Shifted_Griewank) (with Simulated Annealing):

Problem has many wide local minima that are regularly distributed. I failed on a random-based rand1exp strategy with Differential Evolution. Particle Swarm Optimization may be a good approach here but isn't available in Scipy, so I opted for Simulated Annealing. Worked fine at dimension 50 but, for dimension 500, I got stuck multiple times in a close-to-optimum local solution so I finally activated a complementary local search, which reduced a lot the time needed to find the global minimum.

---
[F6 SHIFTED ACKLEY](https://github.com/eIectrai/metaheuristics/tree/master/F6_Shifted_Ackley) (with Simulated Annealing):

Problem has flat outer regions and a deep hole in the center with many spikes. Scipy's Dual Annealing implementation of Simulated Annealing seems well fitted for this problem and came very close to, if not reached, the global minimum without requiring a local search strategy. I kept default temperature, stepsize and acceptance parameters which provide a rather aggressive exploration.

---
[TSP](https://github.com/eIectrai/metaheuristics/tree/master/TSP) (with Ant Colony Algorithm):

Ant Colony Algorithm covers the search space quite fast, which is fine for testing various approaches. I opted for a diversification-based strategy by setting a high independence (beta) level compared to leadership (alpha). Also kept a medium evaporation rate so that ants don't get too distracted by previous paths. Because of that setup there were discrepancies in the results but, within 20 runs for both dimensions 38 and 194, Ant Colony Algorithm offered decent result candidates in comparison with other algorithms tested (Genetic Algorithm and Simulated Annealing).
