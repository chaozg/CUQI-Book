# 2. Running the book code examples


When accessing this book online (as opposed to the PDF version), you will notice that many of the book pages have a power button ⏻ at the top right of the page content. These pages usually contain text and code cells along with the code outputs. The code examples in these pages are complete and fully runnable, see for example section {ref}`BIP_simplest_short`, and you can run them yourself. We recommend using one of these two approaches to achieve that:

- Running the examples on your local machine (preferred)
- Running the examples using the launch button (for quick exploration)

## 2.1. Running the examples on your local machine (preferred)


To run these code examples on your local machine, you will first need to install CUQIpy and its dependencies. CUQIpy installation instructions can be found [here](https://cuqi-dtu.github.io/CUQIpy/user/getting_started.html).

You can then download each page by clicking on the download icon at the top-right corner of the page. The downloaded file will be a Jupyter notebook (.ipynb), which you can run on your local machine.

As an alternative to downloading these examples using the download icon, you can clone the book repository on your local machine and run these examples locally. The examples are in Jupyter notebook format and organized in folders, with each folder corresponding to a chapter. To clone the repository from the command line, run the following command inside the directory where you want to clone the repository:
```bash
git clone https://github.com/CUQI-DTU/CUQI-Book.git
```


## 2.2. Running the examples using the launch button (for quick exploration)
You can run the examples using the launch button (a "rocket" icon at the top-right corner of each code example page), which gives you the option to provide a JupyterHub or BinderHub URL and launch the code examples (the Jupyter notebooks) in a cloud environment. The environment will have the necessary dependencies installed, and you can run the code examples in that environment directly.


### Notes:
Launching the cloud service may take a few minutes to set up the environment. Software tools required for specific examples, such as `FEniCS` and `CIL`, are not installed in the cloud environment by default. For such cases, we recommend running the notebooks on your local machine, where you can install the necessary dependencies.
