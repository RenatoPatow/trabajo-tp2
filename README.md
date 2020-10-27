# trabajo-tp2
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import re\n",
    "import requests"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [],
   "source": [
    "QTL_ID=[]\n",
    "Chromosome=[]\n",
    "Center_cM=[]\n",
    "Range_cM=[]\n",
    "Range_Mbp=[]\n",
    "Significance=[]\n",
    "Publicacion=[]\n",
    "RAZA=[]\n",
    "Pais=[]\n",
    "Gene_Asociado=[]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Introduce una url para acceder a la información de la QTL: https://www.animalgenome.org/cgi-bin/QTLdb/OA/qdetails?QTL_ID=57718\n"
     ]
    }
   ],
   "source": [
    "url = input(\"Introduce una url para acceder a la información de la QTL: \")\n",
    "r = requests.get(url)\n",
    "QTL_information = r.text[:]\n",
    "#print(QTL_information)\n",
    "QTL_ID.append(re.findall('QTL #([0-9]+) Description',QTL_information)[0])\n",
    "Chromosome.append(re.findall('Chromosome.*([0-9])',QTL_information)[0])\n",
    "Center_cM.append(re.findall('Peak Location.*width.*>([0-9.]+)',QTL_information)[0])\n",
    "Range_cM.append(re.findall('QTL Span.*<TD>([0-9.-]+)',QTL_information)[0])\n",
    "Range_Mbp.append(re.findall('QTL Span.*<br>([0-9.-]+)',QTL_information)[0])\n",
    "Significance.append(re.findall('Threshold significance level.*<TD>([A-Za-z]+)',QTL_information)[0])\n",
    "link_1=re.findall('http.*PUBMED_ID=([0-9]+)',QTL_information)\n",
    "Publicacion.append(\"http://www.ncbi.nlm.nih.gov/\"+link_1[0])\n",
    "RAZA.append(re.findall('Breeds.*\\s.*\\s.*href.*>([A-Za-z]+)',QTL_information)[0])\n",
    "p=re.findall('Affiliation.*([ ,])([A-Za-z]+)<.TD',QTL_information)\n",
    "Pais.append((p[0])[1])\n",
    "Gene_Asociado.append(re.findall('Associated Gene.*>([a-z].*)<.font',QTL_information)[0])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "['57718']\n",
      "['2']\n",
      "['68.17']\n",
      "['65.81-70.52']\n",
      "['52.0-55.8']\n",
      "['Significant']\n",
      "['http://www.ncbi.nlm.nih.gov/23810588']\n",
      "['Spanish']\n",
      "['Spain']\n",
      "['n/a']\n"
     ]
    }
   ],
   "source": [
    "print(QTL_ID)\n",
    "print(Chromosome)\n",
    "print(Center_cM)\n",
    "print(Range_cM)\n",
    "print(Range_Mbp)\n",
    "print(Significance)\n",
    "print(Publicacion)\n",
    "print(RAZA)\n",
    "print(Pais)\n",
    "print(Gene_Asociado)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "['13992', '2', '206', '171.7-247.7', '143.9-204.4', 'Suggestive', 'http://www.ncbi.nlm.nih.gov/19849860', 'Merino', 'Australia', 'n/a']\n",
      "['14147', '2', '238.81', '221.5-236.4', '178.8-198.5', 'Significant', 'http://www.ncbi.nlm.nih.gov/20394603', 'Friesian', 'USA', 'n/a']\n",
      "['57681', '2', '0.00', '69.74-69.74', '55.2-55.2', 'Significant', 'http://www.ncbi.nlm.nih.gov/23094085', 'Spanish', 'Spain']\n",
      "['57684', '2', '0.00', '218.39-218.39', '172.5-172.5', 'Significant', 'http://www.ncbi.nlm.nih.gov/23094085', 'Spanish', 'Spain']\n",
      "['57718', '2', '68.17', '65.81-70.52', '52.0-55.8', 'Significant', 'http://www.ncbi.nlm.nih.gov/23810588', 'Spanish', 'Spain', 'n/a']\n"
     ]
    }
   ],
   "source": [
    "csv_file=[]\n",
    "for i in range(len(QTL_ID)):\n",
    "    fila=QTL_ID[i]+ Chromosome[i]+ Center_cM[i]+ Range_cM[i]+ Range_Mbp[i]+ Significance[i]+ Publicacion[i]+ RAZA[i]+ Pais[i]+ Gene_Asociado[i]\n",
    "    csv_file.append(fila)\n",
    "for i in csv_file:\n",
    "    print(i)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "QTL_ID=[]\n",
    "Chromosome=[]\n",
    "Center_cM=[]\n",
    "Range_cM=[]\n",
    "Range_Mbp=[]\n",
    "Significance=[]\n",
    "Publicacion=[]\n",
    "RAZA=[]\n",
    "Pais=[]\n",
    "Gene_Asociado=[]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [],
   "source": [
    "data = {'QTL_ID':QTL_ID,'Chromosome':Chromosome,'Center_cM':Center_cM,'Range_cM':Range_cM,\n",
    "       'Range_Mbp':Range_Mbp,'Significance':Significance,'Publicacion':Publicacion,\n",
    "       'RAZA':RAZA,'Pais':Pais,'Gene_Asociado':Gene_Asociado}\n",
    "df = pd.DataFrame(data,columns=['QTL_ID','Chromosome','Center_cM','Range_cM','Range_Mbp',\n",
    "                                'Significance','Publicacion','RAZA','Pais','Gene_Asociado'])\n",
    "df.to_csv('ADN.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Unnamed: 0</th>\n",
       "      <th>QTL_ID</th>\n",
       "      <th>Chromosome</th>\n",
       "      <th>Center_cM</th>\n",
       "      <th>Range_cM</th>\n",
       "      <th>Range_Mbp</th>\n",
       "      <th>Significance</th>\n",
       "      <th>Publicacion</th>\n",
       "      <th>RAZA</th>\n",
       "      <th>Pais</th>\n",
       "      <th>Gene_Asociado</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>57718</td>\n",
       "      <td>2</td>\n",
       "      <td>68.17</td>\n",
       "      <td>65.81-70.52</td>\n",
       "      <td>52.0-55.8</td>\n",
       "      <td>Significant</td>\n",
       "      <td>http://www.ncbi.nlm.nih.gov/23810588</td>\n",
       "      <td>Spanish</td>\n",
       "      <td>Spain</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Unnamed: 0  QTL_ID  Chromosome  Center_cM     Range_cM  Range_Mbp  \\\n",
       "0           0   57718           2      68.17  65.81-70.52  52.0-55.8   \n",
       "\n",
       "  Significance                           Publicacion     RAZA   Pais  \\\n",
       "0  Significant  http://www.ncbi.nlm.nih.gov/23810588  Spanish  Spain   \n",
       "\n",
       "   Gene_Asociado  \n",
       "0            NaN  "
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "DF = pd.read_csv('ADN.csv')\n",
    "DF"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>QTL_ID</th>\n",
       "      <th>Chromosome</th>\n",
       "      <th>Center_cM</th>\n",
       "      <th>Range_cM</th>\n",
       "      <th>Range_Mbp</th>\n",
       "      <th>Significance</th>\n",
       "      <th>Publicacion</th>\n",
       "      <th>RAZA</th>\n",
       "      <th>Pais</th>\n",
       "      <th>Gene_Asociado</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>UID</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>57718</td>\n",
       "      <td>2</td>\n",
       "      <td>68.17</td>\n",
       "      <td>65.81-70.52</td>\n",
       "      <td>52.0-55.8</td>\n",
       "      <td>Significant</td>\n",
       "      <td>http://www.ncbi.nlm.nih.gov/23810588</td>\n",
       "      <td>Spanish</td>\n",
       "      <td>Spain</td>\n",
       "      <td>NaN</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "     QTL_ID  Chromosome  Center_cM     Range_cM  Range_Mbp Significance  \\\n",
       "UID                                                                       \n",
       "0     57718           2      68.17  65.81-70.52  52.0-55.8  Significant   \n",
       "\n",
       "                              Publicacion     RAZA   Pais  Gene_Asociado  \n",
       "UID                                                                       \n",
       "0    http://www.ncbi.nlm.nih.gov/23810588  Spanish  Spain            NaN  "
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "DF2 = pd.read_csv('ADN.csv',  skiprows=1,            \n",
    "                 names=['UID','QTL_ID','Chromosome','Center_cM','Range_cM','Range_Mbp',\n",
    "                       'Significance','Publicacion','RAZA','Pais','Gene_Asociado'],\n",
    "                 index_col='UID')\n",
    "DF2"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.6"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
