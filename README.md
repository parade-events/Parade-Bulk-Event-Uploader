# Parade Bulk Event Uploader

Simple Python 3 script used to batch upload events to [Parade](https://parade.events/) given a delimited file.

Parade backend is running GraphQL with auth sent via the Authorization header.

## Setup

Utilizes prisma's [python-graphql-client](https://github.com/prisma/python-graphql-client) to wrap the GraphQL requests.  

Install by running `pip install graphqlclient`

## Usage

First, set environment variable `PARADE_JWT` to a valid Parade token.  

Next, edit the `ENDPOINT` and `ORGANIZATION_ID` variables accordingly.

Now execute:

`python3 main.py <INPUT FILE>`

You'll see the the graphQL response, whether that be an error or success message.

![upload-msg](assets/upload-msg.png)

## Input
Read in a CSV file with THIS header, and each column aligned with the following (not trailing `|`):
`title|description|startTime|endTime|location|imageUrl|tags|` 

Each field is delimited by a pipe (`|`).

See the [example file](./example.pipe).


## Tips
A useful excel formula to get times formatted properly. 

**Note**
* +4 to account for Boston time **during** Daylight Savings
* +5 for Boston when **outside** Daylight Savings.

`=CONCATENATE(TEXT(source!C1, "YYYY-MM-DD"),"T",TEXT((source!E1 + TIME(4,0,0)), "hh:mm:ss"), "Z")`

Useful for conditionally adding endTime


`=IF(ISBLANK(source!F1),"",CONCATENATE(TEXT(source!C1, "YYYY-MM-DD"),"T",TEXT((source!F1 + TIME(4,0,0)), "hh:mm:ss"), "Z"))`

