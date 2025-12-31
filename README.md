Counterfactual Simulation: AI-Tax Labor Polarization DiD

Shrey Yadav | IBDP1 | shrey.yadav10@gmail.com

True DGP (Baked-In Parameters)
text
Low-skill AI×Post: β = -0.120
High-skill AI×Post: β = +0.042
AI exposure: N(0.20, 0.15)
N = 100,000 synthetic obs
Results: simulation_results.csv
text
specification        beta    se      N
true_dgp_low        -0.120  0.000 100000
true_dgp_high       +0.042  0.000 100000
recovered_simple    -0.093  0.023 100000
Files
File	Description
simulated_microdata_100k.csv	100k synthetic workers (NOT real CPS)
simulation_results.csv	True vs recovered β's
simulation_script.py	Full reproducible pipeline
Method: Counterfactual DiD | JEL: C53, J24, J31
Replicates: Acemoglu NBER w32487 framework
