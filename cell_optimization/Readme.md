# Cell optimization

More explanation has been given in the geometry optimization section. Here, we just mention some notes on cell optimization. It is better to perform both cell and geometry 
optimization simultaneously. This is done by setting the `TYPE` in `&CELL_OPT` to `DIRECT_CELL_OPT`. As was mentioned in the geometry optimization section, we need accurate forces
so that the optimizer can better optimize the structure. The `STRESS_TENSOR` is needed to compute the pressure for cell optimization. You can also print out the stress as well
using `&STRESS ON` in `&PRINT` section.
