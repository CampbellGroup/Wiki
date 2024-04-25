The DAC ad660 server operates the DAC board on our experiment. a somewhat-detailed breakdown of how the DAC board physically works is available on our lab wiki: http://10.97.112.13:4567/qsim/hardware/electronics/DAC660

the DAC server is quite prone to failure upon [[LabRAD]] startup. There are two main errors that you can receive when starting the server:
- ok_TransferError: try re-plugging the USB and power cycling the DAC board. It may take a few tries
- FPGA not found: check USB continuity and maybe power cycle. It's possible that you may need to do some more intense debugging, connecting to the FPGA via the opalKelly python interface and troubleshooting more directly to try to get the FPGA detected. http://10.97.112.13:4567/opal-kelly-6010 for some starters. 

Some other things to try: 
`sudo chmod -R 777 /dev`
