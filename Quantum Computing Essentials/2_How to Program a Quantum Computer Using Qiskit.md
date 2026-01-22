#### How to program a quantum computer using Qiskit
[![How to program a quantum computer using Qiskit](https://img.youtube.com/vi/Jx7IuJMYtJM/0.jpg)](https://www.youtube.com/watch?v=Jx7IuJMYtJM)

## **Core Quantum Computing Concepts:**

### **1. Qubits vs Classical Bits**
- **Classical bits**: Can only be 0 or 1 (like a regular light switch)
- **Qubits**: Can be 0, 1, or both simultaneously (like a dimmer switch that's partially on and off at the same time)
- **Key difference**: Qubits can exist in multiple states at once, enabling quantum parallelism

### **2. Superposition**
- **What it is**: A qubit being in a combination of 0 and 1 states simultaneously
- **Simple analogy**: Like a spinning coin that's both heads and tails while it spins
- **Result**: When measured, it randomly collapses to either 0 or 1 with certain probabilities
- **Glasp insight**: "Superposition allows quantum computers to process multiple possibilities simultaneously, giving them potential speed advantages for certain problems" (https://glasp.co/reader?url=https%3A%2F%2Fblog.glasp.co%2Fquantum-superposition-explained%2F)

### **3. Quantum Gates**
- **Purpose**: Operations that change qubit states (like logic gates in classical computing)
- **Examples from video**:
  - **Hadamard gate (H)**: Creates superposition (equal 50/50 chance of 0 or 1)
  - **CNOT gate (CX)**: Creates entanglement between two qubits
- **How they work**: Mathematically represented as matrices that transform qubit states

### **4. Entanglement**
- **What it is**: Strong correlation between qubits where the state of one instantly affects another, even at a distance
- **Video example**: When first qubit is measured as 0, second qubit becomes 0; when first is 1, second becomes 1
- **"Spooky action"**: Einstein's term for this non-local connection
- **Glasp highlight**: "Entangled qubits share a single quantum state, meaning measuring one instantly determines the state of the other, regardless of distance" (https://glasp.co/reader?url=https%3A%2F%2Fread.glasp.co%2Fquantum-entanglement-practical%2F)

## **Qiskit Programming Concepts:**

### **5. Quantum Circuit Structure**
```python
# Basic Qiskit program structure:
from qiskit import QuantumCircuit

# Create circuit with 2 qubits and 2 classical bits
qc = QuantumCircuit(2, 2)

# Apply gates
qc.h(0)          # Hadamard on qubit 0 → creates superposition
qc.cx(0, 1)      # CNOT: qubit 0 controls qubit 1 → creates entanglement

# Measure
qc.measure([0, 1], [0, 1])  # Measure qubits → store in classical bits
```

### **6. Registers in Qiskit**
- **Quantum registers**: Hold qubits during computation
- **Classical registers**: Store measurement results (bring quantum info back to classical world)
- **Why both needed**: Quantum states exist during computation, but we need classical bits to read results

### **7. Measurement Behavior**
- **From the example**: When running the program many times:
  - 50% chance of getting "00"
  - 50% chance of getting "11"
  - 0% chance of "01" or "10" (due to entanglement)
- **Important**: Measurement collapses superposition into definite states

## **Practical Programming Insights:**

### **8. Qiskit Architecture Levels**
- **Low-level (Circuit level)**: Direct qubit manipulation (like assembly language)
  ```python
  qc.h(0)  # Direct gate application
  qc.cx(0, 1)
  ```
- **High-level (Algorithm level)**: Pre-built quantum algorithms and integrations
  ```python
  # Example: Quantum machine learning integration
  from qiskit_machine_learning.kernels import QuantumKernel
  from sklearn.svm import SVC
  
  quantum_kernel = QuantumKernel()
  # Use with classical ML algorithms
  ```

### **9. Real-World Application Example**
Quantum computing can enhance classical algorithms:
1. Use quantum circuits to create special "quantum kernels"
2. Integrate with classical libraries like scikit-learn
3. Potentially accelerate machine learning tasks for certain problems

## **Key Takeaways for Beginners:**

1. **Start with simple circuits**: Master basic gates (H, CX) before complex algorithms
2. **Think probabilistically**: Quantum programs give probability distributions, not definite answers
3. **Embrace the weirdness**: Superposition and entanglement are fundamentally different from classical computing
4. **Practical approach**: Use Qiskit's high-level APIs when starting, then learn circuit-level details

## **Common Beginner Questions Answered:**

**Q: Why do we need classical registers if we have qubits?**
A: Qubits exist in quantum states during computation, but when we measure them, we need classical bits to store and process the results in our regular computers.

**Q: What does "50% chance" mean practically?**
A: If you run the same quantum program 1000 times, about 500 times you'll get "00" and about 500 times you'll get "11" (for the example circuit).

**Q: Can I run this on my regular computer?**
A: Yes! Qiskit has simulators that run on classical computers. Actual quantum hardware access is available through IBM Quantum Cloud.

**Q: Why is entanglement useful?**
A: It allows qubits to be correlated in ways impossible classically, enabling algorithms like quantum teleportation and potentially faster problem-solving.

The transcript provides a excellent foundation showing that while quantum programming introduces new concepts (superposition, entanglement), tools like Qiskit make it accessible by providing a Python-based interface similar to classical programming.

Learn more on Glasp: https://glasp.co/reader?url=https://www.youtube.com/watch?v=Jx7IuJMYtJM