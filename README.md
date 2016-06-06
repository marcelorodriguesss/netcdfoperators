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

### NetCDF

#####Exibir cabeçalho do arquivo

$ ncdump -h ifile.nc

#####Exibir pontos de grade

$ ncdump -v x,y ifile

### NCO

#####Renomear variaveis

$ ncrename -v old_var,new_var ifile.nc ofile.nc

#####Calcular média entre arquivos

$ ncea -h ifile1.nc ifile2.nc ofile.nc

#####Extrair variável

$ ncks -v total_resolved_precip,resolved_precip_rate ifile.nc ofile.nc

$ ncks -d x,-38.08 -d y,-5.14 -v temperature ifile.nc ofile.nc

$ ncks -d x,40,60 -d y,40,70 -v temperature ifile.nc ofile.nc

#####Inverter eixos

$ ncpdq -h -a -lat ifile.nc ofile.nc

#####Concatenar arquivos 

$ ncrcat -h 85.nc 86.nc 87.nc 88.nc 89.nc 85-89.nc

#####Renomear atributos de variaveis

$ ncatted -a units,prate,o,c,"mm/day" ifile.nc

$ ncatted -a calendar,time,o,c,"360" ifile.nc

$ ncatted -a units,time,o,c,"hours since 1989-2-28 0" ifile.nc

$ ncatted -a calendar,time,o,c,"360" ifile.nc

$ ncatted -O -a units,x,o,c,degree_east pcp.nc

$ ncatted -O -a units,y,o,c,degree_north pcp.nc

#####Soma, subtração, multiplição e divisão

http://stderr.org/doc/nco/html/ncbo-netCDF-Binary-Operator.html

$ ncbo --op_typ=add 1.nc 2.nc 3.nc

$ ncbo --op_typ='-' 1.nc 2.nc 3.nc ou ncdiff 1.nc 2.nc 3.nc

$ ncbo --op_typ=mlt 1.nc 2.nc 3.nc

$ ncbo --op_typ=/ 1.nc 2.nc 3.nc

### OpenGrADS e Lats4D

http://opengrads.org/doc/scripts/lats4d/lats4d.html

######Extrair/Salvar variável diária no formato binário
```
open ifile.ctl
set dfile 1
set x 1 145
set y 1 73
set z 1
set fwrite -sq ofile.bin
set gxout fwrite
day = 1
while(day <= 10)
  set t 'day'
  d sea_press
day=day+1
endwhile
disable fwrite
quit
``` 
ou
```
lats4d.sh -format sequential -i ifile.ctl -o ofile.bin
````

#####Salvar NetCDF no formato binário
sdfopen ifile.nc
set fwrite ofile.bin
set gxout fwrite
d pcp
disable fwrite
quit

#####Salvar dado no formato NetCDF
open ifile.ctl
set x 1 10
set y 1 10
set z 1
set sdfwrite ofile.nc
sdfwrite pcp
quit

ou 

lats4d.sh -format netcdf -i ifile.ctl -o ofile


