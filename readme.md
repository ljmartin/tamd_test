# Testing TAMD
Speed comparison for simulations with/without TAMD. Simulation object has a CustomBondForce attached that measures the distance between two ions (sodium and chloride) in solution. The equilibrium distance, i.e. the collective variable, is set by a global parameter. This global parameter is also the "coordinate" of a fictitious, massive particle that diffuses in response to 1) almost adiabatic attachment to the collective variable, and 2) brownian (infinite friction) attachment to a heat bath

# normal:
Stepping is performed as usual, i.e. `simulation.step(1000)`. The collective variable is just held constant. 

# tamd:
Simulation is run step by step, i.e. `for _ in 1000: simulation.step(1); ...;`. After each step, the integrator returns the derivative of the bond force wrt ion distance (the collective variable), which is used to calculate a new position for the fictitious particle. The new position is sent back to the integrator by setting the global parameter. 
