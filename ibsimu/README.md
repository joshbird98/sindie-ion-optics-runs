# IBSimu source used for the builds

`libibsimu-1.0.6dev_89c1280.tar.xz`: IBSimu 1.0.6dev, git snapshot 89c1280, as supplied by Josh on
23 October 2026 (SourceForge is not reachable from every machine that builds it). Build objects and
the GTK front end's generated files are removed; the sources are otherwise unchanged. IBSimu is by
Taneli Kalvas and is distributed under the GNU General Public License, version 2 (COPYING inside the
archive).

    sha256 f7c8dad0fd62ae5ab1f63073ffe56100db762a2df3e429dcaf6254849d05cacc

`analysis/ion_optics/build_ibsimu.sh` in PhD-Thesis builds it (with system packages, or without root
from the conda-forge environment in `analysis/ion_optics/cluster/environment.yml`).
