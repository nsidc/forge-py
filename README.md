# forge-py

Tool to generate footprints

## NSIDC prototyping notes

This repository was forked from PO.DAAC's original `forge-py` project.  The tool
assumes spatial information is read from a netCDF file rather than from an auxiliary
text file.  For the purposes of this experiment I added command line options to
support logic to handle spatial input from a text file containing only a series
of lon/lat values. The option to create Geojson output was also hard-coded.
The script as-is generates a polygon, not Gpolygon with internal GRings.

The default alpha values appear to generate a convex hull, or at least not a concave one.
A modified alpha value of 2.5 creates a decent simple concave-ish hull outline.

Code was also added to separate the application configuration from the dataset
configuration.

If we revisit this python foot printing code, see the concave hull example using
shapely and Delaunay triangulation at https://gist.github.com/dwyerk/10561690

### Running from the command line

You will need to be in a `python` 3.11 environment (*not* 3.12, due to the
elimination of `imp` in 3.12). Install poetry using the official
installer at https://python-poetry.org/docs/#installing-with-the-official-installer (do *not* use `pipx`).

Once `poetry` is installed, then install `forge-py` dependencies and run the script:

```
poetry install
poetry shell
python ./podaac/forge_py/cli.py --granule_config ./samples/irmcr2_20191109_01.cfg --spatial ./samples/IRMCR2_20191109_01.csv.spatial --output_file geojson.json --config configs/config.yml
```

The specified configuration file and command line options will write log output to the local file `log.txt`.
Spatial output is written (as geojson) to local file `geojson.json`
