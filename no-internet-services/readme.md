## Simple example for docker compose containers with and without internet

Some times you want to isolate the containers, in order to improve security.

This example is based on the reponse in [StackOverflow](https://stackoverflow.com/questions/39913757/restrict-internet-access-docker-container) about resticting access. A simple example only with one docker compose from the response is: 

'''
version: '3'

services:
  outgoing-wont-work:
    image: alpine
    networks:
      - no-internet
    command: ping -c 3 google.com # will crash

  internal-will-work:
    image: alpine
    networks:
      - no-internet
    command: ping -c 3 internal-and-external

  internal-and-external:
    image: alpine
    networks:
      - no-internet
      - internet
    command: ping -c 3 google.com

networks:
  no-internet:
    driver: bridge
    internal: true
  internet:
    driver: bridge
'''

## Using docker compose

In order to run the example enter to each folder starting with network and start the services with 'docker compose up -d'