# Tensorflow_quantum_project

1. Problem Setup:
Quantum computers promise to revolutionize fields like medicine and materials science by tackling problems impossible for classical computers. However, today's quantum devices operate in the "NISQ" (Noisy Intermediate-Scale Quantum) era. Qubits are not error corrected, and therefore perform imperfect operations within a limited coherence time[1]. Like static interfering with a clear radio signal, quantum noise – random errors from the environment and imperfect hardware – constantly disrupts quantum computations, limiting their accuracy and reliability.

• Core Idea: Investigate how quantum noise impacts the ability of a hybrid quantum-classical model to perform a quantum control task.

•	Goal: Train a classical neural network (the "controller") to output quantum gate parameters that prepare the qubit in a target state (e.g., +Z or -Z eigenstate), despite a fixed, unknown initial "miscalibration" rotation applied to the qubit.

![image](https://github.com/user-attachments/assets/8d11a370-e52f-4229-8bdc-9df44aeac15c)

2. Project Phases & Experiments

  •	Baseline (Noiseless):
 
-	Build the hybrid model using the noiseless full_circuit and tfq.layers.ControlledPQC (default noiseless backend).

-	Train it on the commands [0, 1] and target expectations [1, -1]. The circuits_input will be two copies of an empty circuit (or the miscalibration_circuit if kept separate).

-	Evaluate the final loss and check the output expectations.

  •	Noisy Scenario:
 
-	Define a noise level p.

-	Build the hybrid model using Tensorflow_Quantum Library

-	Train this model using the same commands and targets.

-	Evaluate the final loss and check the output expectations.

  •	Noise Impact Analysis:
 
-	Plot the final loss achieved during training vs. the noise level p.

-	Plot the final output expectation values achieved for command 0 and command 1 vs. p (compare to the ideal +1 and -1).

-	Analyze how noise degrades the controller's ability to learn the correction.

  •	Parameter Tuning:
 
-	Experiment with the controller NN architecture (number of layers/neurons) and the optimizer's learning rate to see if performance under noise can be improved.

  •	Error Mitigation (ZNE):
 
-	Take a trained noisy model (from step 2 at a specific p).

-	Implement ZNE during inference/evaluation.
