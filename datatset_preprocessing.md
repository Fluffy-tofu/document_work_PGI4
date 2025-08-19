### Preprocessing the Spiking Heidelberg Digits (SHD) Dataset

### Project Goal

My goal was to take a look at the **Spiking Heidelberg Digits (SHD)** dataset and think of a good way to input it into a Spiking Neural Network.

***

### Dataset Overview

The Dataset was given in an `.h5` file. It represents spoken German and English digits as neural spikes. The raw data consists of three main components:
-   **`units`:** The sound was converted into 700 unit ids using an artifical model mimicing parts of the inner ear and the ascending auditory pathway.
-   **`times`:** The exact time in milliseconds when the spike occurred.
-   **`labels`:** The corresponding digit (0-9 for German, 10-19 for English).

The Data is has the big temporal component of what unit was triggered at what time making it a good training set for SNNs.

***

### Data Exploration and Visualization

To understand the dataset I loaded the Dataset and made some Graphs for it:

1.  **Histograms:** I first created two histograms, one for the `times` data and one for the `unit` IDs.
    * **Time Histogram:** The histogram of spike times showed that the vast majority of spikes occurred within the first 600 milliseconds of each recording. This indicated that the later parts of the recordings contained little to no useful information and could maybe just be cut off.
    * **Unit ID Histogram:** The histogram for the unit IDs showed that the spikes were heavily concentrated in unit IDs greater than 200. This meant that the first 200 or so unit ids were rarely active. 

    [Image placeholder for unit ID and time histograms]

2.  **Scatter Plots:** Next, I used scatter plots to visualize the relationship between time and unit ID for individual samples.
    * **Initial Scatter Plot:** My initial plot, showing all samples, was a dense cloud of points. It confirmed the sparsity of the data but provided little in the way of discernible patterns. It was a good starting point to confirm the nature of the data.
    * **Filtered Scatter Plot:** To find more meaningful patterns, I filtered the data to show only the English digits (labels 10-19). This plot was still very cluttered, but it did a better job of highlighting the most active unit IDs, which appeared to be clustered above 150. This reinforced my earlier finding from the histograms and provided a concrete basis for reducing the number of input neurons.

    [Image placeholder for scatter plot of filtered data for English digits]

***

### Addressing the Neuron Input Problem

The primary challenge was the sheer number of input neurons (700 total), which would make any subsequent SNN model unnecessarily large and inefficient. My data exploration confirmed that many of these neurons were inactive. The goal of the following steps was to systematically reduce the number of input neurons while preserving the unique temporal spike patterns for each digit. I achieved this through **filtering, vectorization, and pooling**.

1.  **Vectorization:** To make the data usable for an SNN, I converted the spike lists into a uniform format. I created a dictionary of matrices, where each key corresponded to a spoken digit. Each matrix had `unit IDs` on one axis and `time steps` on the other. I filled in the matrix with a **'1'** if a spike occurred at that specific unit ID and time, and a **'0'** otherwise. I also applied a crucial optimization here: I **cut off the first 150 unit IDs**, which my visualizations showed were largely inactive.
    * **Matrix vs. Scatter Plot:** To verify this transformation, I created a plot that placed the vectorized matrix side-by-side with its original scatter plot. This confirmed that the conversion was accurate and that the key spike patterns were maintained.

    [Image placeholder for comparison between spike matrix and scatter plot]

2.  **Pooling:** As a final step to further reduce the number of input neurons and make the data more robust, I applied a **pooling** operation.
    * **The Kernel:** I used a 3x3 kernel to downsample the matrices. This kernel essentially combines the activity of a small group of adjacent neurons over a short period of time into a single new "neuron." If the number of spikes within the 3x3 area exceeded a specific **threshold**, the new neuron would fire.
    * **Testing Thresholds:** I plotted matrices with different pooling thresholds (1, 2, 3, and 4) to determine the best value. This visualization was essential as it showed the trade-off: a low threshold could introduce noise, while a high one could lose important data. My analysis indicated that a threshold of **2 or 3** was optimal for preserving the critical patterns while effectively reducing the dimensionality.

    [Image placeholder for pooling threshold comparison]

This multi-step preprocessing pipeline successfully converted the raw, sparse data into a compact and efficient format. By intelligently culling inactive neurons and applying pooling, I significantly reduced the dimensionality of the input data, setting the stage for building an SNN.
