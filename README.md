# magic_card_detector
Python implementation of a Magic: the Gathering card segmentation and recognition

General description of the algorithms and several example can be found in my blog:
https://tmikonen.github.io/quantitatively/2020-01-01-magic-card-detector/

Forked 2022-10-30 from: https://github.com/tmikonen/magic_card_detector 
 for the root card detector
Forked 2023-09-25 from: https://github.com/matthew-buglass/mtg_inventory_system
 for the base inventory system

Now I'm hoping to get it running in my environment and add instructions.

## Developing

Assuming docker and docker-compose are installed,

1. Create the env vars
`touch .env`
```
POSTGRES_PASSWORD=[anything-you-want]
POSTGRES_DB=postgres
POSTGRES_USER=postgres

DB_HOST=mtg-postgres [name of docker container in docker-compose]
DB_PORT=5432

```

2. `docker compose up -d`

3. Check to make sure it's running
`docker logs mtg-inventory-system`

4. Setup an admin user account

Get to the container shell
`docker exec -it mtg-inventory-system bash`

Run migrations on database
`python manage.py migrate`

Import card data
`python manage.py update_all_cards`
`python manage.py get_card_prices`

Create the admin account
`python manage.py createsuperuser --username=[your-username] --email=[your-email]`
Enter a new password for your account, when prompted
Repeat the password, when prompted.

5. Log in with newly created account
http://127.0.0.1:8000/login/

ToDo:
- There seems to be a version conflict between psql installed on the python container and the version of postgres on the DB container.
  - Perhaps update python container to psql client 14 (preference)
  - Perhaps force older postgres on DB container