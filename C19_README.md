#################################################
#############################################
# Example for RUNNING FUNCTION C19Proj_function
#################################################

DATA= read.table(file.choose(), header=T, sep="\t")
REGIONS.info_i= read.table(file.choose(), header=T, sep="\t")
REGIONS.info=REGIONS.info_i[REGIONS.info_i$REGION=="GO",]


C19Proj_function(Data.Table=DATA,
                 Tabela.info=REGIONS.info,
                 DATA3=TRUE, 
                 Col.region=2,#2, 3
                 Col.date=3,#3, 1
                 Col.ac.inf=5,#5, 4
                 ISOL=45,
                 DIAS_REC=14,
                 DIAS_MORT=8,
                 MVD=5,  
                 DRI=68, 
                 NOT=0.14, 
                 POPAFE=0.10,  
                 R0e=F, 
                 HR=0.13, 
                 LR=0.045,
                 DR =0.0185, #c(0.0237, 0.057),         
                 TIPO_GRAFICO="curto.prazo",
                 TIPO_PAINEL="Group", 
                 YLIM_prop=0.75,
                 XLIMcp=120, #curta.duração, 
                 XLIMlp=260, #longa.duração, leitos, picos          
                 ReportTable=T,
                 TableFile="C:/Users/lgcar/OneDrive/Ambiente de Trabalho/COVID19/Tabelas_previsoes/ReportTable_EDU_11Maio.txt") 


#############################################

## INPUTS TABLES
#################
#Data.Table # Table with 4 columns (Date,	Day,	REGION,	Cases)
#Date - actual date
#Day - number of the days since case 1 (Day 1 = day of first case) 
#Cases - information on number of cases per day

#Tabela.info # Table with at least 5 columns (REGION, GROUP, D1, D2, POPULATION)
#REGION - region of interest (e.g. state of Brazil or a country)
#GROUP - group of focal regions (e.g. regions of Brazil, or continent), this column is not yet used in the current version of the function
#D1 - Date of the first case in the focal region (REGION)
#D2 - Date where the second model (orange lines) should start (e.g. date of implementation of isolation measures or date where 50 cases were reached)


#DATA3==TRUE, # when DATA3=T the model uses D3 from information table and generates all estimates for orange lines (after isolation) based on data starting on this date


## Columns
#Col.region - column with the code of the geographic region (country, state, city that will be analysed) 
#Col.date   - column with date information
#Col.ac.inf - column with information on accumulated infection number

  

## CONSTANTS to define support capacity (K): K = POPULATION*NOT*POPAFE
#######################################################################
  
  
#NOT #0.14 (DEFAULT) proportion of infected people that are known (notified) Li et al. 2020 10.1126/science.abb3221 (86% subnotificacao)
#POPAFE #0.44 (DEFAULT) #proportion of the total population that is thought to be infected in the end of the epidemy  
#DIAS_REC=14  - average number of days required for recovery
#DIAS_MORT  - average number of days for death to occur
#MVD=7   - # meia-vida virus - average virus life, days since infection started  until confirmation happens
#DRI=45  - day (since day one) when relaxation of isolation wants to be applied


## CONSTANTS to define number of hospitalized people, and number of critical cases
#HR - proportion of infected people (reported cases) that need hospitalization
#LR - proportion of infected people (reported cases) that need intensive care
#DR - death rate


## CONSTANTS to estimate number of infected people in a given date (acumulated number of infected people - solved cases)
################################################################################################################################
#DIAS_REC # DEFAULT=14; average time for recovery 
#DIAS_MORT # DEFAULT=8; average time for death
#ISOL - maximum level of isolation

## GRAPH PRESENTATION PARAMETERS
#################################
#TIPO_GRAFICO #OPTIONS: "curto.prazo"; # if "curto.prazo" short term graphs for the first 60 days will be generated presenting estimates of R0 current growth rate, inflexion point date (peak of epidemy), date for reaching max number of cases (end of epidemy)
                         # "longo.prazo"; 
                         # "picos" (DEFAULT), # this will present the curve of infected people per day (accumulated infected people - resolved cases)
                        # "leitos"           # this will present the progression of hospitalized people and demand of intensive care beds according to HR and LR

#TIPO_PAINEL # OPTIONS: "Region" (DEFAULT); "Group", if "Region" it will generate a Figure with 9 graphs; if "REGION" it will generate a Figure with as many graphs as 'those 'REGIONs' in the data table (max of 4) 
#YLIM_prop # 0.75 (DEFAULT) constant to define YLIM for peak graphs (proportion of K) 

## REPORT TABLE PARAMETERS
#################################
#Report Table # OPTIONS: F (DEFAULT - Table is not generated), T (Table is generated)
#TableFile # path and name of file to be generated

