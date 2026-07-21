From the meeting on Feb, 18th 2025, here are some of the software stacks that we are interested in contributing to.

<table>
  <thead>
    <tr>
      <th>Software Project</th>
      <th>Description</th>
      <th>Interests</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://github.com/shibatch/sleef">SLEEF</a></td>
      <td>Used by PyTorch and other projects for complex math operations (quad, dft, fft) on CPU. It supports RISC-V fully since <a href="https://github.com/shibatch/sleef/releases/tag/3.6.1">3.6.1</a></td>
      <td>Qualcomm - Ludovic Henry<br>SiFive - Hong-Rong Hsu</td>
    </tr>
    <tr>
      <td><a href="https://github.com/OpenMathLib/OpenBLAS">OpenBLAS</a></td>
      <td>Industry standard for BLAS operations. Used by every AI/ML framework out there. It supports RISC-V RVV 128/256/512 bits already. The implementation is currently optimized for large square matrices which aren't the typical shapes in AI/ML workloads. There is already support to pick different kernels based on the matrix shape for x86, we need to leverage that mechanism on RISC-V as well</td>
      <td>Microchip - Ken Unger<br>Qualcomm - Ludovic Henry<br>SiFive - Hong-Rong Hsu<br>ZTE - Yunxiang Jia</td>
    </tr>
    <tr>
      <td><a href="https://gitlab.com/libeigen/eigen">Eigen</a></td>
      <td>Eigen is a C++ template library for linear algebra: matrices, vectors, numerical solvers, and related algorithms. Used by PyTorch, Tensorflow, and Tensorflow-Lite (LiteRT). It doesn't support RISC-V at all at the moment. There is an <a href="https://gitlab.com/libeigen/eigen/-/issues/2842">open issue</a> and a corresponding <a href="https://gitlab.com/libeigen/eigen/-/merge_requests/1687">open MR</a> but there hasn't been much activity over the past 5 months</td>
      <td>Microchip - Ken Unger<br>Qualcomm - Ludovic Henry</td>
    </tr>
    <tr>
      <td><a href="https://github.com/oneapi-src/oneDNN">oneDNN</a></td>
      <td>It provides a DNN API (similar to cuDNN) and it's used in lots of places. It is already functional on RISC-V (<a href="https://github.com/oneapi-src/oneDNN?tab=readme-ov-file#system-requirements">per the documentation</a>), but it is still experimental and it's unclear how optimized it is with RVV.</td>
      <td>Qualcomm - Ludovic Henry<br>ISCAS - fei zhang<br>ZTE - Yunxiang Jia</td>
    </tr>
    <tr>
      <td><a href="https://github.com/google/XNNPACK">XNNPACK</a></td>
      <td>There has been contributions from SiFive and Microchip, but contributions are slow to get merged. Contributions are being tracked in <a href="https://docs.google.com/spreadsheets/d/1PZAzBSqpdwoNgkxgrnmf5DDsZBzC_GEh/view">this spreadsheet</a>. We need to identify which intrinsics are critical to the models we care for. Notes: Microchip: "No intent to work on F16; not a high priority for us - just F32 and int8 support"</td>
      <td>Microchip - Ken Unger<br>Qualcomm - Ludovic Henry<br>SiFive - Hong-Rong Hsu<br>Andes - Alan Quey-Liang Kao</td>
    </tr>
    <tr>
      <td><a href="https://github.com/pytorch/pytorch">PyTorch CPU</a></td>
      <td>This work focused on PyTorch operators themselves, and not the dependencies used by PyTorch like OpenAI Triton, SLEEF, etc. A blocker is (was?) the availability of hardware to test on. Patches from SiFive were rejected for this reason. There is an <a href="https://github.com/pytorch/pytorch/pull/143979">open PR</a> to integrate cross-compilation support to CI. There would still be work to optimize many of the PyTorch Operators using RVV</td>
      <td>Alibaba - Binhua Wang<br>Qualcomm - Ludovic Henry<br>SiFive - Hong-Rong Hsu<br>ISCAS - fei zhang<br>ZTE - Yunxiang Jia</td>
    </tr>
    <tr>
      <td><a href="https://github.com/openxla/iree">IREE</a></td>
      <td>Interest is in the context of using it as a PyTorch compiler backend (see <a href="https://pytorch.org/docs/stable/torch.compiler.html">torch.compiler</a> for details)</td>
      <td>Andes - Ruinland Tsai<br>SiFive - Hong-Rong Hsu</td>
    </tr>
    <tr>
      <td><a href="https://github.com/triton-lang/triton">OpenAI Triton</a></td>
      <td></td>
      <td>BOSC - David Gao</td>
    </tr>
    <tr>
      <td><a href="https://github.com/scikit-learn/scikit-learn">Scikit-Learn</a></td>
      <td>scikit-learn already works out-of-the-box on RISC-V. However to reach better performance, Intel provides <a href="https://pypi.org/project/scikit-learn-intelex/">scikit-learn-intelex</a> on x86 which is based on oneDAL. Rivos has already done the work to accelerate oneDAL on RISC-V, but we now need to provide a similar plugin to scikit-learn-intelex for RISC-V to bridge the worlds of scikit-learn and oneDAL.</td>
      <td>Qualcomm - Ludovic Henry</td>
    </tr>
    <tr>
      <td><a href="https://github.com/google-ai-edge/LiteRT">LiteRT (Tensorflow-Lite)</a></td>
      <td></td>
      <td>SiFive - Hong-Rong Hsu<br>Andes - Alan Quey-Liang Kao</td>
    </tr>
    <tr>
      <td><a href="https://github.com/pytorch/executorch">Executorch</a></td>
      <td></td>
      <td>Andes - Alan Quey-Liang Kao</td>
    </tr>
    <tr>
      <td><a href="https://github.com/numpy/numpy">Numpy</a></td>
      <td>NumPy is the fundamental package for scientific computing with Python. With the Highway library, NumPy can leverage RVV (RISC-V Vector Extension) acceleration on RISC-V architectures.</td>
      <td>ISCAS - wang yang</td>
    </tr>
    <tr>
      <td><a href="https://github.com/zilliztech/knowhere">Knowhere</a></td>
      <td><strong>Knowhere</strong> is the core component of the open-source vector database <strong>Milvus</strong>, specializing in high-performance vector search. By integrating multiple underlying libraries (e.g., FAISS, HNSW, Annoy, etc.), it provides a unified vector computing interface for upper-layer applications.</td>
      <td>ISCAS - Liuyudong</td>
    </tr>
    <tr>
      <td><a href="https://github.com/alibaba/MNN">MNN</a></td>
      <td><strong>MNN</strong> is a highly efficient and lightweight open-source deep learning framework, specializing in high-performance on-device inference and training. By integrating multiple hardware backends (e.g., CPU, GPU, NPU, etc.), it provides a unified interface for efficiently executing deep learning tasks.</td>
      <td>ISCAS - Liuyudong<br>ISCAS - Hebo</td>
    </tr>
    <tr>
      <td><a href="https://github.com/milvus-io/milvus">Milvus</a></td>
      <td><a href="https://milvus.io/">Milvus</a> is a high-performance vector database built for scale. It powers AI applications by efficiently organizing and searching vast amounts of unstructured data, such as text, images, and multi-modal information.</td>
      <td>ISCAS - Liuyudong</td>
    </tr>
    <tr>
      <td><a href="https://github.com/facebookresearch/faiss">Faiss</a></td>
      <td><strong>Faiss</strong> is a library for efficient similarity search and clustering of dense vectors, developed by Facebook AI Research. It enables fast nearest neighbor search in high-dimensional spaces, making it suitable for applications such as image retrieval, recommendation systems, and large-scale machine learning.</td>
      <td>ISCAS - Liuyudong</td>
    </tr>
    <tr>
      <td><a href="https://github.com/vllm-project/vllm">vLLM</a></td>
      <td><strong>vLLM</strong> is an open-source library for high-speed inference and serving of large language models (LLMs). Originally developed at UC Berkeley, its standout feature is <strong>PagedAttention</strong>, an innovative memory management algorithm inspired by operating system paging. This technology efficiently organizes the model's Key-Value (KV) cache, drastically reducing memory fragmentation and waste, which allows for significantly higher throughput compared to standard inference engines.</td>
      <td>ISCAS - Liuyudong</td>
    </tr>
  </tbody>
</table>
