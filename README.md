# Assignment-2.1
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p style=\"text-align:center\">\n",
    "    <a href=\"https://skills.network\" target=\"_blank\">\n",
    "    <img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png\" width=\"200\" alt=\"Skills Network Logo\">\n",
    "    </a>\n",
    "</p>\n",
    "\n",
    "<h1 align=center><font size = 5>Assignment: SQL Notebook for Peer Assignment</font></h1>\n",
    "\n",
    "Estimated time needed: **60** minutes.\n",
    "\n",
    "## Introduction\n",
    "Using this Python notebook you will:\n",
    "\n",
    "1.  Understand the Spacex DataSet\n",
    "2.  Load the dataset  into the corresponding table in a Db2 database\n",
    "3.  Execute SQL queries to answer assignment questions \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Overview of the DataSet\n",
    "\n",
    "SpaceX has gained worldwide attention for a series of historic milestones. \n",
    "\n",
    "It is the only private company ever to return a spacecraft from low-earth orbit, which it first accomplished in December 2010.\n",
    "SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars wheras other providers cost upward of 165 million dollars each, much of the savings is because Space X can reuse the first stage. \n",
    "\n",
    "\n",
    "Therefore if we can determine if the first stage will land, we can determine the cost of a launch. \n",
    "\n",
    "This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.\n",
    "\n",
    "This dataset includes a record for each payload carried during a SpaceX mission into outer space.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Download the datasets\n",
    "\n",
    "This assignment requires you to load the spacex dataset.\n",
    "\n",
    "In many cases the dataset to be analyzed is available as a .CSV (comma separated values) file, perhaps on the internet. Click on the link below to download and save the dataset (.CSV file):\n",
    "\n",
    " <a href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/data/Spacex.csv\" target=\"_blank\">Spacex DataSet</a>\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Requirement already satisfied: sqlalchemy==1.3.9 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (1.3.9)\n"
     ]
    }
   ],
   "source": [
    "!pip install sqlalchemy==1.3.9\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Connect to the database\n",
    "\n",
    "Let us first load the SQL extension and establish a connection with the database\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "tags": []
   },
   "outputs": [],
   "source": [
    "%load_ext sql"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "tags": []
   },
   "outputs": [],
   "source": [
    "import csv, sqlite3\n",
    "\n",
    "con = sqlite3.connect(\"my_data1.db\")\n",
    "cur = con.cursor()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "tags": []
   },
   "outputs": [],
   "source": [
    "!pip install -q pandas==1.1.5"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Connected: @my_data1.db'"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql sqlite:///my_data1.db"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "/home/jupyterlab/conda/envs/python/lib/python3.7/site-packages/pandas/core/generic.py:2615: UserWarning: The spaces in these column names will not be changed. In pandas versions < 0.14, spaces were converted to underscores.\n",
      "  method=method,\n"
     ]
    }
   ],
   "source": [
    "import pandas as pd\n",
    "df = pd.read_csv(\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/labs/module_2/data/Spacex.csv\")\n",
    "df.to_sql(\"SPACEXTBL\", con, if_exists='replace', index=False,method=\"multi\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "**Note:This below code is added to remove blank rows from table**\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "(sqlite3.OperationalError) table SPACEXTABLE already exists\n",
      "[SQL: create table SPACEXTABLE as select * from SPACEXTBL where Date is not null]\n",
      "(Background on this error at: http://sqlalche.me/e/e3q8)\n"
     ]
    }
   ],
   "source": [
    "%sql create table SPACEXTABLE as select * from SPACEXTBL where Date is not null"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Tasks\n",
    "\n",
    "Now write and execute SQL queries to solve the assignment tasks.\n",
    "\n",
    "**Note: If the column names are in mixed case enclose it in double quotes\n",
    "   For Example \"Landing_Outcome\"**\n",
    "\n",
    "### Task 1\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "##### Display the names of the unique launch sites  in the space mission\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Launch_Site</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>VAFB SLC-4E</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>KSC LC-39A</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>CCAFS SLC-40</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('CCAFS LC-40',), ('VAFB SLC-4E',), ('KSC LC-39A',), ('CCAFS SLC-40',)]"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT DISTINCT Launch_Site FROM SPACEXTABLE;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\n",
    "### Task 2\n",
    "\n",
    "\n",
    "#####  Display 5 records where launch sites begin with the string 'CCA' \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Launch_Site</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('CCAFS LC-40',),\n",
       " ('CCAFS LC-40',),\n",
       " ('CCAFS LC-40',),\n",
       " ('CCAFS LC-40',),\n",
       " ('CCAFS LC-40',)]"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT Launch_Site FROM SPACEXTABLE WHERE Launch_Site LIKE 'CCA%' LIMIT 5;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 3\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "##### Display the total payload mass carried by boosters launched by NASA (CRS)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Total_Payload_Mass_KG</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>48213</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[(48213,)]"
      ]
     },
     "execution_count": 29,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT SUM(PAYLOAD_MASS__KG_) AS Total_Payload_Mass_KG FROM SPACEXTABLE WHERE Payload LIKE 'SpaceX CRS%';\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 4\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "##### Display average payload mass carried by booster version F9 v1.1\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Average_Payload_Mass_KG</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>2534.6666666666665</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[(2534.6666666666665,)]"
      ]
     },
     "execution_count": 30,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT AVG(PAYLOAD_MASS__KG_) AS Average_Payload_Mass_KG FROM SPACEXTABLE WHERE Booster_Version LIKE 'F9 v1.1%';"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 5\n",
    "\n",
    "##### List the date when the first succesful landing outcome in ground pad was acheived.\n",
    "\n",
    "\n",
    "_Hint:Use min function_ \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>First_Successful_Landing_Date</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>2015-12-22</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('2015-12-22',)]"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT MIN(Date) AS First_Successful_Landing_Date FROM SPACEXTABLE WHERE Landing_Outcome = 'Success (ground pad)';"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 6\n",
    "\n",
    "##### List the names of the boosters which have success in drone ship and have payload mass greater than 4000 but less than 6000\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Booster_Version</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>F9 FT B1022</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 FT B1026</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 FT  B1021.2</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 FT  B1031.2</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('F9 FT B1022',), ('F9 FT B1026',), ('F9 FT  B1021.2',), ('F9 FT  B1031.2',)]"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT Booster_Version FROM SPACEXTABLE WHERE Landing_Outcome = 'Success (drone ship)' AND PAYLOAD_MASS__KG_ > 4000 AND PAYLOAD_MASS__KG_ < 6000;\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 7\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "##### List the total number of successful and failure mission outcomes\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Mission_Outcome</th>\n",
       "            <th>Total_Count</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Success</td>\n",
       "            <td>98</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('Success', 98)]"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT Mission_Outcome, COUNT(*) AS Total_Count FROM SPACEXTABLE WHERE Mission_Outcome IN ('Success', 'Failure') GROUP BY Mission_Outcome;\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 8\n",
    "\n",
    "\n",
    "\n",
    "##### List the   names of the booster_versions which have carried the maximum payload mass. Use a subquery\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Booster_Version</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1048.4</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1049.4</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1051.3</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1056.4</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1048.5</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1051.4</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1049.5</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1060.2 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1058.3 </td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1051.6</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1060.3</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>F9 B5 B1049.7 </td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('F9 B5 B1048.4',),\n",
       " ('F9 B5 B1049.4',),\n",
       " ('F9 B5 B1051.3',),\n",
       " ('F9 B5 B1056.4',),\n",
       " ('F9 B5 B1048.5',),\n",
       " ('F9 B5 B1051.4',),\n",
       " ('F9 B5 B1049.5',),\n",
       " ('F9 B5 B1060.2 ',),\n",
       " ('F9 B5 B1058.3 ',),\n",
       " ('F9 B5 B1051.6',),\n",
       " ('F9 B5 B1060.3',),\n",
       " ('F9 B5 B1049.7 ',)]"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT Booster_Version FROM SPACEXTABLE WHERE PAYLOAD_MASS__KG_ = (SELECT MAX(PAYLOAD_MASS__KG_) FROM SPACEXTABLE);\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 9\n",
    "\n",
    "\n",
    "##### List the records which will display the month names, failure landing_outcomes in drone ship ,booster versions, launch_site for the months in year 2015.\n",
    "\n",
    "**Note: SQLLite does not support monthnames. So you need to use  substr(Date, 6,2) as month to get the months and substr(Date,0,5)='2015' for year.**\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Month</th>\n",
       "            <th>Landing_Outcome</th>\n",
       "            <th>Booster_Version</th>\n",
       "            <th>Launch_Site</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>01</td>\n",
       "            <td>Failure (drone ship)</td>\n",
       "            <td>F9 v1.1 B1012</td>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>04</td>\n",
       "            <td>Failure (drone ship)</td>\n",
       "            <td>F9 v1.1 B1015</td>\n",
       "            <td>CCAFS LC-40</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('01', 'Failure (drone ship)', 'F9 v1.1 B1012', 'CCAFS LC-40'),\n",
       " ('04', 'Failure (drone ship)', 'F9 v1.1 B1015', 'CCAFS LC-40')]"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT substr(Date, 6, 2) AS Month,Landing_Outcome,Booster_Version,Launch_Site FROM SPACEXTABLE WHERE substr(Date, 0, 5) = '2015'AND Landing_Outcome = 'Failure (drone ship)';\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Task 10\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "##### Rank the count of landing outcomes (such as Failure (drone ship) or Success (ground pad)) between the date 2010-06-04 and 2017-03-20, in descending order.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "metadata": {
    "tags": []
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * sqlite:///my_data1.db\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Landing_Outcome</th>\n",
       "            <th>Outcome_Count</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>No attempt</td>\n",
       "            <td>10</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Success (drone ship)</td>\n",
       "            <td>5</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Failure (drone ship)</td>\n",
       "            <td>5</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Success (ground pad)</td>\n",
       "            <td>3</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Controlled (ocean)</td>\n",
       "            <td>3</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Uncontrolled (ocean)</td>\n",
       "            <td>2</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Failure (parachute)</td>\n",
       "            <td>2</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Precluded (drone ship)</td>\n",
       "            <td>1</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('No attempt', 10),\n",
       " ('Success (drone ship)', 5),\n",
       " ('Failure (drone ship)', 5),\n",
       " ('Success (ground pad)', 3),\n",
       " ('Controlled (ocean)', 3),\n",
       " ('Uncontrolled (ocean)', 2),\n",
       " ('Failure (parachute)', 2),\n",
       " ('Precluded (drone ship)', 1)]"
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql SELECT Landing_Outcome,COUNT(*) AS Outcome_Count FROM SPACEXTABLE WHERE Date BETWEEN '2010-06-04' AND '2017-03-20' GROUP BY Landing_Outcome ORDER BY Outcome_Count DESC;\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Reference Links\n",
    "\n",
    "* <a href =\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20String%20Patterns%20-%20Sorting%20-%20Grouping/instructional-labs.md.html?origin=www.coursera.org\">Hands-on Lab : String Patterns, Sorting and Grouping</a>  \n",
    "\n",
    "*  <a  href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20Built-in%20functions%20/Hands-on_Lab__Built-in_Functions.md.html?origin=www.coursera.org\">Hands-on Lab: Built-in functions</a>\n",
    "\n",
    "*  <a  href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Labs_Coursera_V5/labs/Lab%20-%20Sub-queries%20and%20Nested%20SELECTs%20/instructional-labs.md.html?origin=www.coursera.org\">Hands-on Lab : Sub-queries and Nested SELECT Statements</a>\n",
    "\n",
    "*   <a href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Module%205/DB0201EN-Week3-1-3-SQLmagic.ipynb\">Hands-on Tutorial: Accessing Databases with SQL magic</a>\n",
    "\n",
    "*  <a href= \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/Module%205/DB0201EN-Week3-1-4-Analyzing.ipynb\">Hands-on Lab: Analyzing a real World Data Set</a>\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Author(s)\n",
    "\n",
    "<h4> Lakshmi Holla </h4>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Other Contributors\n",
    "\n",
    "<h4> Rav Ahuja </h4>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Change log\n",
    "| Date | Version | Changed by | Change Description |\n",
    "|------|--------|--------|---------|\n",
    "| 2021-07-09 | 0.2 |Lakshmi Holla | Changes made in magic sql|\n",
    "| 2021-05-20 | 0.1 |Lakshmi Holla | Created Initial Version |\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## <h3 align=\"center\"> © IBM Corporation 2021. All rights reserved. <h3/>\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python",
   "language": "python",
   "name": "conda-env-python-py"
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
   "version": "3.7.12"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
