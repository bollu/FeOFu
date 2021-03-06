[![Join the chat at https://gitter.im/Compiler-Seminar/community](https://badges.gitter.im/Compiler-Seminar/community.svg)](https://gitter.im/Compiler-Seminar/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

# FeOFu - Compiler Seminar
Features of the Future

In this repository we'd like to collect ideas that would lead to better compilers for existing languages, better future programming languages, better APIs and better performance software solutions in the future.

**This semester we hold regular meetings every Tuesday between 16:00-18:00 CEST on google meet**

Join the chat at https://gitter.im/Compiler-Seminar/community

Mailing list: https://groups.google.com/d/forum/compiler-seminar-budapest


### 2020 spring semester:

- *15 April 2020*, **AST modeling in Soufflé Datalog**

  *Presenter:* Csaba Hruska  
  *Recommended reading:* https://souffle-lang.github.io/tutorial

- *22 April 2020*, **Lifetime analysis for C++**

  *Presenter:* Gábor Horváth  
  *Recommended reading:* Chapter 3 and Appendix A of https://www.dropbox.com/s/4iog86ljrhyehrp/thesis.pdf?dl=0 
  *Note:* The reading above is a draft, any feedback is welcome.
  
- *29 April 2020*, **Introduction to type inference (and program inference)**

  *Presenter:* András Kovács
  
- *6 May 2020*, **(Glued) evaluation and normalization for lambda calculus**

  *Presenter:* András Kovács
  
- *13 May 2020*, **Symbolic Execution**

  *Presenter:* Gábor Horváth  
  *Recommended reading:*
   - [A Survey of Symbolic Execution Techniques](https://arxiv.org/pdf/1610.00502.pdf)
   - [Incorrectness Logic](https://research.fb.com/publications/incorrectness-logic/)

- *20 May 2020*, **Symbolic Execution - taint analysis, constraint manager in Clang**

  *Presenter:* Balázs Benics  
  *Recommended reading:*
  - [Inspection the use of static code analysis to automatically detect security issues](https://edit.elte.hu/xmlui/bitstream/handle/10831/46472/szakdolgozat.pdf)
  - [An user configurable clang static analyzer taint checker](https://www.researchgate.net/publication/312938554_An_user_configurable_clang_static_analyzer_taint_checker)

- *27 May 2020*, **Code devirtualization, packers**

  *Presenter:* Dávid Török  
  *Recommended reading:*
   - [Unpacking Virtualization Obfuscators](https://www.usenix.org/legacy/event/woot09/tech/full_papers/rolles.pdf)
   - [Syntia: Synthesizing the Semantics  of Obfuscated Code](https://www.usenix.org/system/files/conference/usenixsecurity17/sec17-blazytko.pdf)

<hr>

### 2019 spring semester:


- *18 February 2019*, **Dataflow analysis**

  *Presenter:* Gábor Horváth  
  *Recommended reading:* [Engineering a Compiler](https://www.amazon.com/Engineering-Compiler-Keith-Cooper/dp/012088478X) Chapter 9.2

- *25 February 2019*, **LambdaGen and Structured Recursion Schemes**

  *Presenter:* Dániel Berényi  
  *Recommended reading:* [Eric Niebler: F-algebras and C++](http://ericniebler.com/2013/07/16/f-algebras-and-c/)

- *04 March 2019*, **Using SMT solvers in Compilers**

  *Presenter:* Réka Kovács  
  *Recommended reading:* [link](https://docs.google.com/document/d/1E1ebMVt--vRLUhlbhjoAtceZn7PbHW31yCv_g3Cvovs)

- *11 March 2019*, **GRIN and Heap Points To Analysis** [slides](https://docs.google.com/presentation/d/1QsZ3Kyy3XIco-qba1biRmzuMzz8o2uCBqA9DMtnqP2c/edit?usp=sharing)

  *Presenter:* Csaba Hruska  
  *Recommended reading:*  <a href="http://nbviewer.jupyter.org/github/grin-tech/grin/blob/master/papers/The GRIN Project.pdf">The GRIN Project</a>  

- *18 March 2019*, **Points To Analysis Overview** [slides](http://web.cs.iastate.edu/~weile/cs513x/2.PointerAnalysis.pdf)

  *Presenter:* Csaba Hruska  
  *Recommended reading:*
    - [Tutorial / Survey](https://yanniss.github.io/points-to-tutorial15.pdf) '15
    - [Points-to Analysis in Almost Linear Time](https://www.cs.cornell.edu/courses/cs711/2005fa/papers/steensgaard-popl96.pdf) '96
    - [Fast and Accurate Flow-Insensitive Points-To Analysis](http://www.cs.utexas.edu/users/pingali/CS380C/2007fa/papers/popl97.pdf) '97
    - [The ant and the grasshopper:fast and accurate pointer analysis for millions of lines of code](https://www.cs.utexas.edu/~lin/papers/pldi07.pdf) '07
    - [A GPU Implementation of Inclusion-based Points-to Analysis](https://userweb.cs.txstate.edu/~mb92/papers/ppopp12.pdf) '12

- *25 March 2019*, **Non-intrusive testing methods**, **Chains of Recurrences**

  *Presenter:* Gábor Márton  
  *Presenter:* Gábor Horváth  
  *Recommended reading:*
    - [Chains of Recurrences](http://gsd.web.elte.hu/lectures/bolyai/2018/ChainofRecurrences/10.1.1.43.8188.pdf)
  

- *1 April 2019*, SYCL

  *Presenter:* Máté Ferenc Nagy-Egri
  *Recommended reading:*
    - [OpenCL overview](https://www.khronos.org/opencl/)
    - Minimal OpenCL app: [C](https://github.com/Wigner-GPU-Lab/Teaching/tree/master/GPGPU1/OpenCL/OpenCL-C-API) and [C++](https://github.com/Wigner-GPU-Lab/Teaching/tree/master/GPGPU1/OpenCL/OpenCL-C%2B%2B-API)
    - [OpenCL-GL interop sample](https://github.com/Wigner-GPU-Lab/Teaching/tree/master/GPGPU1/OpenCL-GL/Qt/NBody)

- *8 April 2019*, SYCL (cont.)

  *Presenter:* Máté Ferenc Nagy-Egri
  *Recommended reading:*
    - [SYCL overview](https://www.khronos.org/sycl/)
    - [SYCL SAXPY sample](https://github.com/MathiasMagnus/Test-Applications/tree/master/SYCL-SAXPY)
    - [SYCL-CL-GL interop sample](https://github.com/Wigner-GPU-Lab/Teaching/tree/master/GPGPU1/SYCL-GL/Qt/NBody)
    - [ComputeCpp](https://www.codeplay.com/products/computesuite/computecpp)
    - [Intel SYCL implementation](https://github.com/intel/llvm/)

- *29 April 2019*, **Efficient Program Analysis with Datalog**

  *Presenter:* Csaba Hruska  
  *Recommended reading:*
    - [Introduction to Datalog](http://pages.cs.wisc.edu/~paris/cs784-s17/lectures/lecture7.pdf)
    - [Pointer Analysis tutorial with Datalog](https://yanniss.github.io/points-to-tutorial15.pdf)
    - [Soufflé (docs)](https://souffle-lang.github.io/docs/home)
    
 
- *20 May 2019*, **MLIR**

  *Presenter:* Gabor Horvath  
  *Links:*
    - [EuroLLVM MLIR Keynote](https://llvm.org/devmtg/2019-04/talks.html#Keynote_1)
    - [EuroLLVM MLIR Tutorial](https://llvm.org/devmtg/2019-04/talks.html#Tutorial_1)
    - [Github](https://github.com/tensorflow/mlir)
