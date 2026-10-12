# ASUS ROG Flow Z13, 2026-10-12, git workloads

Same box and settings as `z13-2026-10-11`. `smolvm-1.27.0-libkrun183.csv` is one
`.\run.ps1 -Distro AlpineBench -Git -Runs 3` with the smolvm 1.27.0 release and the
krun.dll from smol-machines/libkrun#183. The 1.27.0 release alone cannot run `git.sh`
on a Windows folder: `git clone` fails there (stale inode path after rename, and
symlinks that need Developer Mode).

git's own repository, v2.45.0, checkout to v2.47.0. Medians of 3, seconds:

| workload | Windows folder WSL2 | Windows folder smolvm | guest disk WSL2 | guest disk smolvm |
|---|---|---|---|---|
| clone | 32.9 | 19.6 | 0.93 | 0.50 |
| status, first | 1.42 | 0.83 | 0.13 | 0.05 |
| status ×10 | 11.4 | 3.82 | 0.34 | 0.50 |
| checkout v2.45 → v2.47 | 7.26 | 5.23 | 0.26 | 0.21 |
| log --stat -n 2000 | 3.43 | 1.99 | 1.18 | 0.94 |
| grep | 3.64 | 2.00 | 0.11 | 0.07 |
| rm -rf | 5.84 | 3.45 | 0.13 | 0.06 |

WSL2 is ahead on one row: repeated `git status` on the guest disk.
