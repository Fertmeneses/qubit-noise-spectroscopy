# Deep Learning applied to Spectral Imaging of Magnetic Noise

**[Website in development...]**

As a postdoc in **The City College of New York** (CCNY, USA), I have combined my experimental skills in quantum sensing along with artificial intelligence (AI) techniques. In collaboration with **University College London** (UCL, UK) and **Universidad Nacional de Córdoba** (UNC, Argentina), we published a research article titled **Toward Deep-Learning-Assisted Spectrally Resolved Imaging of Magnetic Noise**, in the journal *Physical Review Applied* in 2022.

[Link to the research article](https://journals.aps.org/prapplied/abstract/10.1103/PhysRevApplied.18.024004) 👈🏽.

The full list of authors include:
* Fernando Meneses (CCNY).
* David F. Wise (UCL).
* Daniela Pagliero (CCNY).
* Pablo R. Zangara (UNC).
* Siddharth Dhomkar (UCL).
* Carlos A. Meriles (CCNY).

The main concept of the work was to we probe the response of **quantum defects in diamond** in the presence of a **magnetic environment** and implement a **deep neural network** to extract information about the **noise spectral density**. Our artificial intelligence method was compared to traditional approaches, demonstrating a **better performance and more precise results**.

<center><figure>
  <img src="https://github.com/Fertmeneses/qubit-noise-spectroscopy/blob/main/assets/Image_Concept.jpg?raw=true" alt="Conceptual image"> 
  <figcaption><sup>Conceptual image, AI-generated using the prompt "A small diamond on top of a flat metallic surface with unknown content underneath, with energy waves".</sup></figcaption>
</figure></center>

## Introduction

**Quantum sensing** is a powerful tool where the theory of quantum mechanics can be applied to measure physical properties, for example detecting subtle changes in magnetic fields with great precision. A well-established platform for this technology is the **nitrogen-vacancy (NV) center in diamond**, a specific type of defect within the diamond lattice, in which a nitrogen atom has replaced a carbon atom, next to a spot in which there is a missing carbon atom (vacancy). **This NV defect hosts a quantum system that is extremely sensitive to magnetic fields**, and can be manipulated optically to read out very small variations in the magnetic environment.

**Magnetic signals are usually convoluted with noise originated by random magnetic fluctuations**. This noise, tipycally seen as an obstacle for measurements, can also become a **valuable source of information**, as it may encode critical properties of the local composition and structure of a sample. Consequently, understanding and characterizing the **noise spectral density** is a powerful tool to extract detailed information about a sample's physical properties.

The **problem of decoding magnetic noise** has long been critical for many fields, as it is fundamental for practical applications. **Traditional approaches**, which rely on theoretical models and numerical methods, have made significant progress in the area, but they face **large limitations due to oversimplifications or the extensive experimental data that is required**, which usually compromises the accuracy of the results.

In our research, we address the challenge of **reconstructing the noise spectral density from experimental magnetic measurements**, emphasizing the case of colored noise, where random magnetic fluctuations are mostly distributed within a frequency range. The novelty of our work comes with the application of artificial intelligence tools, showing that **deep learning algorithms can efficiently reconstruct the noise spectral density, employing a minimal experimental dataset**. Our results have benchmarked those of equivalent methodologies using only theoretical and numerical methods, highlighting the **great potential of combining AI-based methods with quantum sensing**.

<center><figure>
  <img src="https://github.com/Fertmeneses/qubit-noise-spectroscopy/blob/main/assets/Noise_PSD_examples.png?raw=true" alt="Signal and Power Spectral Density examples"> 
  <figcaption><sup>(Left) Examples of magnetic signals as a function of time for different colored noises. (Right) Power Spectral Density associated to those signals, with the central (color) frequency indicated by a dashed line, and the half-width bandwidth at half-maximum by a shaded area.</sup></figcaption>
</figure></center>

## Deep Learning algorithm

In order to determine the Power Spectral Density (PSD) from magnetic signals, we have designed an **AI Autoencoder algorithm**. This program takes **magnetic timeseries as input data** and **determines the PSD of the underlying magnetic noise** in the frequency space. 

The idea behind the **autoencoding process** is to first **extract the essential information from the magnetic timeseries** into a reduced representation, and then **expand it to the frequency domain** to reconstruct the PSD of the magnetic noise. The main tools in the process are the **one-dimensional (1D) Convolutional Layers**, which scan the input data with 1D filters and **extract the most relevant features**. The Autoencoder algorithm consists in two main structures: first the **Encoder**, which combines 1D Convolutional Layers with **Max-Pooling layers to reduce the information in each step**, while preserving the critical features; and then the **Decoder**, which instead uses **Up-sampling layers to progressively expand the data**.

<center><figure>
  <img src="https://github.com/Fertmeneses/qubit-noise-spectroscopy/blob/main/assets/AI_algorithm.png?raw=true" alt="AI algorithm"> 
  <figcaption><sup>Autoencoder algorithm: the input magnetic timeseries is first encoded into a reduced representation by one-dimensional (1D) Convolutional and Max-Pooling layers, and then expanded into the frequency domain by 1D-Convolutional and Upsampling layers, finally returning the noise Power Spectral Density.</sup></figcaption>
</figure></center>

Our algorithm has a **Deep Leaning structure** (meaning many internal layers) which **requires training on a large dataset**, having at least a few tens of thousands of samples, in order to optimize its numerous internal parameters. As our application aims to **predict the PSD of real magnetic measurements**, the ideal dataset would comprise a large collection of experimental measurements. However, acquiring a single timeseries sample can take several minutes, then **measuring just 10.000 samples non-stop would take more than a month**.

An **alternative solution for generating a large dataset** is to use **simulations** that reproduce the experimental conditions within a range of colored noises. Although simulations cannot perfectly replicate real-world conditions, the AI algorithm can still learn to identify patterns and generalize its knowledge to real data. In our work, we have simulated a **set of 500.000 samples**, 80% used for training and 20% for testing.

## Results

The colored noise studied in this work is within the range of tens to a few hundreds of kHz. At this frequency, the **Hahn Echo control sequence** (experimental technique) allows us to **measure the *relaxation time* of the NV defects** and to **determine the *coherence curve***, which goes from a state of maximum to minimum information regarding the quantum state of the NV defects. The shape of this coherence curve is **strongly affected by the magnetic noise**, which is the main principle that we use in our AI application to determine the Power Spectral Density for each particular noise.

On the left column of the Figure below, there are **three examples of coherence curves**, our magnetic signals in this case, affected by different colored noises. The real PSD is computed on the right by solid lines, showing **distinct signatures for each noise**. When the input data is processed by our **Deep Learning algorithm**, the **PSD predictions** (green dashed lines in central column) are **very close to the true values**. As a comparison, we also show the results obtained by the **traditional approach** commonly used for this experimental technique (red dotted lines in right column), barely indicating the distribution of the noise spectrum and **evidencing poor accuracy**.

<center><figure>
  <img src="https://github.com/Fertmeneses/qubit-noise-spectroscopy/blob/main/assets/AI_results.png?raw=true" alt="AI vs traditional results"> 
  <figcaption><sup>Results for the determination of Power Spectral Density (PSD) of different colored noises from magnetic signals (left column), using either Artificial Intelligence (central column) or a traditional approach (right column). The better agreement of the AI method with the true PSD (solid lines) becomes evident in all cases.</sup></figcaption>
</figure></center>




Our results demonstrate the potential of the AI method applied to experimental techniques, and there is ample room for improvement. On the one hand, the quality of the magnetic timeseries strongly depends on the number of averages during the measurements. At the expense of more meausuring time, cleaner input data can be prepared for the AI autoencoder, which will translate into more precise outputs. On the other hand, augmenting the training dataset with more frequency and bandwidth conditions can also enhance the predictions. In all cases, more resources must be employed to improve the AI predictions, and the limit is set by the user and precision level required by the application.

On the other hand, the AI method has demonstrated an improvement over its traditional counterpart, employing theory and numerical methods. Usually, the level of accuracy attained by our algorithm requires more complex experiments compared to the simple Hahn Echo. Our AI algorithm can also benefit from those experiments, and a broader ranges of colored main frequencies and bandwidth can be studied.




## Conclusions

In this research, we have developed an AI autoencoder algorithm that can be combined with magnetic platforms, such as the NV centers in diamond, to determine the Power Spectral Density of the noise behind a magnetic signal. The demonstrated superiority of our method compared to traditional numerical solutions invites to consider the great potential of AI applied to experimental techniques. As determining the PSD for magnetic signals is key to several applications, the AI algorithm can be tailored according to the problem's need to achieve the desired accuracy, improving the efficiency known so far by other approaches.

![Banner](httplink)

