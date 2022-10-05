# git-stats

A simple Python utility to retrieve history of a Git project. Looking
at the project history, it counts the number of commits authored and
signed-off by a group of developers. The group of developers is defined
in one or several 'identity' files. It can be used to retrieve detailed
commit information as well (number of changed lines, date, ...).

# Installation

This script requires Python3. To install all dependencies using pip:

    pip install -r requirements.txt

# Usage

    $ ./git-stats -h
    usage: git-stats [-h] [-v] [-i IDENTITY [IDENTITY ...]] [-g [GROUPS ...]] [-r REFSPEC] [-s [{summary,commits} ...]]
    
    optional arguments:
      -h, --help            show this help message and exit
      -v, --verbose         enable verbose output
      -i IDENTITY [IDENTITY ...], --identity IDENTITY [IDENTITY ...]
                            Identity files
      -g [GROUPS ...], --groups [GROUPS ...]
                            restrict developers from these groups
      -r REFSPEC, --refspec REFSPEC
                            refspec to extract commits
      -s [{summary,commits} ...], --show [{summary,commits} ...]
                            List of results/stats to display

# Identity file

The 'identity' file is a Yaml file that contains record for each developer.
A developer data consists of the following:
* Name
* One or several email addresses
* One or several 'groups'. A 'group' can be used to represent an affiliation
for a specific developer. A group includes a date range, if the commit was
done during this date range, then the developer is marked as 'affiliated'
to this group. git-stat can filter commits based on group.

Here is a template identity file:

    John Doe:
      emails:
        - john.doe@linaro.org
        - john@doe.com
      groups:
        - linaro-teamA:
            start: 2010-01-01
        - linaro-teamB:
            start: 2016-01-01
    Jane Doe:
      emails:
        - jane.doe@linaro.org
      groups:
        - linaro-teamC:
            start: 2020-01-01

Note: It is possible to use a Python regular expression in the 'emails' field, using this syntax:
emails:
    - /<reg expressions>/

E.g.
emails:
    - /.*@linaro.org/
