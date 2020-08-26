---
layout: post
title: "Fermion to Qubit - Extra dimension"
date: 2020-07-26
---
<SCRIPT SRC='https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML'></SCRIPT>
<SCRIPT>MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}})</SCRIPT>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    "HTML-CSS": { scale: 165}
  });
</script>

<style>
@keyframes atom {
  from { transform: none; }
  to { transform: translateY(-10px); }
}
@keyframes electron-circle1 {
  from { transform: rotateY(70deg) rotateZ(20deg); }
  to { transform: rotateY(70deg) rotateZ(380deg); }
}
@keyframes electron1 {
  from { transform: rotateZ(-20deg) rotateY(-70deg); }
  to { transform: rotateZ(-380deg) rotateY(-70deg); }
}
@keyframes electron-circle2 {
  from { transform: rotateY(60deg) rotateX(60deg) rotateZ(-30deg); }
  to { transform: rotateY(60deg) rotateX(60deg) rotateZ(330deg); }
}
@keyframes electron2 {
  from { transform: rotateZ(30deg) rotateX(-60deg) rotateY(-60deg); }
  to { transform: rotateZ(-330deg) rotateX(-60deg) rotateY(-60deg); }
}
@keyframes electron-circle3 {
  from { transform: rotateY(-60deg) rotateX(60deg) rotateZ(100deg); }
  to { transform: rotateY(-60deg) rotateX(60deg) rotateZ(460deg); }
}
@keyframes electron3 {
  from { transform: rotateZ(-100deg) rotateX(-60deg) rotateY(60deg); }
  to { transform: rotateZ(-460deg) rotateX(-60deg) rotateY(60deg); }
}


.atom {
  margin: 50px auto;
  width: 220px;
  height: 220px;
  position: relative;
  top: 0px; right: 100px;
  animation: atom 1s ease-in-out infinite alternate;
  perspective: 300px;
  transform-style: preserve-3d;
}
.atom:before {
	content: '';
	position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 20px;
  height: 20px;
  border-radius: 10px;
  background: #555;
}
.atom .electron {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
	width: 100px;
  height: 100px;
  border-radius: 50px;
  border: 2px solid #666;
  transform-style: preserve-3d;
}
.atom .electron:before {
	content: '';
  position: absolute;
  top: -4px;
  left: 0;
  right: 0;
  margin: auto;
  width: 8px;
  height: 8px;
  border-radius: 4px;
  background: #666;
  transform-origin: 50% 50% 0;
}
.atom .electron:nth-child(1) {
  transform: rotateY(70deg) rotateZ(20deg);
  animation: electron-circle1 3s linear infinite;
}
.atom .electron:nth-child(2) {
  transform: rotateY(60deg) rotateX(60deg) rotateZ(-30deg);
  animation: electron-circle2 3s linear infinite;
}
.atom .electron:nth-child(3) {
  transform: rotateY(-60deg) rotateX(60deg) rotateZ(100deg);
  animation: electron-circle3 3s linear infinite;
}
.atom .electron:nth-child(1):before {
  transform: rotateZ(-20deg) rotateY(-70deg);
  animation: electron1 3s linear infinite;
}
.atom .electron:nth-child(2):before {
  transform: rotateZ(30deg) rotateX(-60deg) rotateY(-60deg);
  animation: electron2 3s linear infinite;
}
.atom .electron:nth-child(3):before {
  transform: rotateZ(-100deg) rotateX(-60deg) rotateY(60deg);
  animation: electron3 3s linear infinite;
}

.image {
   content:url("https://sahilgulania.github.io/blog/Bloch_sphere.svg");
   width: 200px;
   position: relative;    
   top: 0px; left: 250px; 
}

</style>
<div class="atom">
  <div class="electron"></div>
  <div class="electron"></div>
  <div class="electron"></div>
<div class="image"></div>
</div>

Hello All,                                                                      
                                                                                
In this blog, I would like to explain one caveat in fermion to qubits mapping. 
There exist many types of fermionic algebra mapping to qubits algebra. 
Jordan-Wigner(JW), Parity(P) and Bravyi-Kitaev(BK) transformation are well known to 
perform this task. Consider, H<sub>2</sub> example in a minimal basis(STO-3G). 

One starts by mapping four spin orbitals to four qubits either via JW or P or BK transformation.
It does not just allow access to the fermionic Hamiltonian of two electrons in a four basis but provides access to all the possible combinations of electron configurations. The initial problem was to solve the electronic Hamiltonian of dimension six, and when mapped to qubit Hamiltonian, its size becomes 16. The rest extra ten dimensions are nothing but configurations corresponding to zero, one, three, and four-electron solutions in the same basis. 

$$ 2^4 = C_0^4 + C_1^4 + C_2^4 + C_3^4 + C_4^4  $$

$$ 2^4 = 1 + 4 + 6 + 4 + 1 = 16  $$

Therefore, when performing VQE to find the ground state, one must prepare the initial state carefully. If the initial state can access states with a total number of electrons different than two, it will converge to that partition sector. 

