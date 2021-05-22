\ifndef{robotWirelessBgplvm}
\define{robotWirelessBgplvm}


\include{_datasets/includes/robot-wireless-data.md}

\editme

\subsection{Bayesian GP-LVM fit to the Robot Wireless Data}



\notes{Set up a Bayesian GP-LVM with four latent dimensions.}

\setupcode{import GPy}

\code{model = GPy.models.BayesianGPLVM(data['Y'], 4, num_inducing=25)}

\notes{Optimize the model.}

\code{model.optimize(messages=True, max_f_eval=10000)}

\setupplotcode{from matplotlib import pyplot as plt
import mlai.plot as plot
import mlai.mlai as ma}

\plotcode{fig, ax = plt.subplots(figsize=plot.big_figsize)
model.plot_latent(ax=ax)
ma.write_figure('robot-wireless-bgplvm.svg',
                directory='\writeDiagramsDir/gplvm')}

\figure{\includediagram{\diagramsDir/gplvm/robot-wireless-bgplvm}{60%}}{Visualisation of the latent space of the Bayesian GP-LVM model applied to the robot wirless data.}{robot-wireless-bgplvm}


\endif