# NetCDF Operators - Manipulação Arquivos NetCDF

### CDO

#####Calcular U e V a partir do divergente e da vorticidade.

$ cdo dv2uv ifile.nc ofile.nc

#####Transformar uma grade Spectral em uma grade Gaussiana.

$ cdo sp2gp ifile.nc ofile.nc

#####Converter de GRIB para NetCDF.

$ cdo -r -f nc -t echam4 copy ifile.nc ofile.grb

#####Converter de GRIB2 para NetCDF.

$ cdo -f nc copy ifile.grib2 ofile.nc

#####Calcular média diária

$ cdo daymean ifile.nc ofile.nc

#####Calcular média mensal

$ cdo monmean ifile.nc ofile.nc

#####Calcular anomalia

$ cdo ydaysub ifile.nc climatology.nc anomaly.nc 

#####Calcular pentadas

$ cdo timselmean,5 ifile ofile

#####Concatenar arquivos

$ cdo cat ifile1.nc ifile2.nc ofile.grib2

#####Selecionar passos de tempo

$ cdo seltimestep,1/372 ifile.nc ofile.nc

#####Calcular a somar dos passos de tempo

$ cdo timselsum,1,2,3 ifile.nc ofile.nc

#####Exibir informações para cada campo do arquivo

$ cdo info ifile.nc
  
#####Calcular diferença entre arquivos

$ cdo diff ifile1 ifile2
  
#####Recortar/Selecionar região e salvar em outro arquivo

$ cdo sellonlatbox,120,-90,20,-20 ifile ofile
  
#####Calcular média entre arquivos

$ cdo ensmean ifile1.nc ifile2.nc ifile3.nc ifile4.nc ifile5.nc ifile6.nc ofile.nc

$ cdo ensavg ifile1.nc ifile2.nc ifile3.nc ifile4.nc ifile5.nc ifile6.nc ofile.nc

#####Calcular número de períodos consecutivos menor que X

Exemplo: Número de períodos de seca com mais de 5 dias.

$ cdo eca_cdd[,5] ifile.nc ofile.nc

#####Interpolar uma grade Gaussiana qualquer (e.g. 384x190-cfs) para (128x64-echam)

$ cdo remapbil,r128x64 ifile.nc ofile.nc

#####Calcular correlação entre dois arquivos

$ cdo timcor ifile1.nc ifile2.nc ofile.nc 

#####Extrair, de um série temporal completa, períodos sazonais.

Exemplo: extrair DJF

$ cdo selmon,12,01,02 ifile.nc ofile.nc 

#####Calcular a soma entre arquivos

$ cdo add ifile1 ifile2 ofile

$ cdo add ifile3 -add ifile1 ifile2 ofile
