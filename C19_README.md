########################################################
####   EXAMPLE for RUNNING C19Proj_function

DATA= read.table(file.choose(), header=T, sep="\t")
REGIONS.info_i= read.table(file.choose(), header=T, sep="\t")
REGIONS.info=REGIONS.info_i[REGIONS.info_i$REGION=="GO",]


C19Proj_function(Data.Table=DATA, Tabela.info=REGIONS.info, DIAS_REC=14,
                           NOT=0.14, POPAFE=0.44,R0e=T,
                           TIPO_GRAFICO="curto.prazo",TIPO_PAINEL="Group", YLIM_prop=0.75,
                           ReportTable=F,TableFile="ReportTable.txt") 




## INPUTS TABLES
#################
# Data.Table # Table with 4 columns (Date,	Day,	REGION,	Cases)
#Date - actual date
#Day - number of the days since case 1 (Day 1 = day of first case) 
#Cases - information on number of cases per day

# Tabela.info # Table with at least 5 columns (REGION, GROUP, D1, D2, POPULATION)
#REGION - region of interest (e.g. state of Brazil or a country)
#GROUP - group of focal regions (e.g. regions of Brazil, or continent), this column is not yet used in the current version of the function
#D1 - Date of the first case in the focal region (REGION)
#D2 - Date where the second model (orange lines) should start (e.g. date of implementation of isolation measures or date where 50 cases were reached)
#POPULATION

## CONSTANTS to define support capacity (K): K = POPULATION*NOT*POPAFE
#######################################################################

#NOT #0.14 (DEFAULT) proportion of infected people that are known (notified) Li et al. 2020 10.1126/science.abb3221 (86% subnotificacao)
#POPAFE #0.44 (DEFAULT) #proportion of the total population that is thought to be infected in the end of the epidemy  

## CONSTANTS to estimate number of infected people in a given date (acumulated number of infected people - solved cases)
################################################################################################################################
#DIAS_REC # DEFAULT=14; average time for cases to be solved (cured or death); 14 is the default assuming that with proper medicine deaths will be avoided 

## GRAPH PRESENTATION PARAMETERS
#################################
# TIPO_GRAFICO #OPTIONS: "curto.prazo"; "longo.prazo"; "picos" (DEFAULT), if "curto.prazo" short term graphs for the first 60 days will be generated presenting estimates of R0 current growth rate, inflexion point date (peak of epidemy), date for reaching max number of cases (end of epidemy)  
# TIPO_PAINEL # OPTIONS: "Regiao" (DEFAULT); "Region", if "Region" it will generate a Figure with 9 graphs; if "REGION" it will generate a Figure with as many graphs as 'those 'REGIONs' in the data table (max of 4) 
# YLIM_prop # 0.75 (DEFAULT) constant to define YLIM for peak graphs (proportion of K) 

## REPORT TABLE PARAMETERS
#################################
# Report Table # OPTIONS: F (DEFAULT - Table is not generated), T (Table is generated)
# TableFile # path and name of file to be generated
