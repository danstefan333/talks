\ifndef{osuRun1Bgplvm}
\define{osuRun1Bgplvm}

\include{_datasets/includes/osu-run1-data.md}

\editme

\subsection{OSU Run 1 Motion Capture Data with Bayesian GP-LVM}

\setupcode{from GPy.models import BayesianGPLVM
import numpy as np}


\code{Q = 6
kernel = GPy.kern.RBF(Q, lengthscale=np.repeat(.5, Q), ARD=True)
model = BayesianGPLVM(data['Y'], Q,
                      init="PCA",
                      num_inducing=20, kernel=kernel)

model.data = data
model.likelihood.variance = 0.001}

\code{model.optimize('bfgs', messages=verbose, max_iters=5e3, bfgs_factor=10)}

\setupplotcode{import matplotlib.pyplot as plt
import mlai.plot as plot
import mlai.mlai as ma}

\setupplotcode{%matplotlib notebook}

\setupplotcode{import numpy as np}

\plotcode{fig, _ = plt.subplots(figsize=plot.big_wide_figsize)
latent_axes = fig.add_subplot(131)
sense_axes = fig.add_subplot(132)
viz_axes = fig.add_subplot(133, projection='3d')

model.plot_latent(ax=latent_axes)
latent_axes.set_aspect('equal')

y = model.Y[:1, :].copy()

data_show = GPy.plotting.matplot_dep.visualize.stick_show(y, connect=data['connect'], viz_axes)
dim_select = GPy.plotting.matplot_dep.visualize.lvm_dimselect(model.X.mean[:1, :].copy(), model, data_show, latent_axes=latent_axes, sense_axes=sense_axes)

ma.write_figure(figure=fig,
                  filename='osu-run1-bgplvm.svg', 
				  directory = '\writeDiagramsDir/bgplvm')}


\newslide{OSU Run 1 Bayesian GP-LVM}

\figure{\includediagram{\diagramsDir/gplvm/osu-run1-bgplvm}{80%}}{Gaussian process latent variable model visualisation of OSU motion capture data set.}{osu-run1-data}


\endif