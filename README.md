# Ganbreeder RURLPARK
RURLPARK is an eight feature GAN Breeder Genomics Organization
This turn key app is a generative adversarial network conceptual application with genomic AI features for GAN's to solve any domain specific example based problem that fits within theory of Cognitive Architecture governing what the users are thinking while playing with the application.

This approach gamifies user interaction using labeling, selection and speciation where species of assets are created.  

Level of sophistication keeps with the persistent AI space which in GANbreeder is the adjusted weight of feature genes which contribute to transform a visual 2D world.

RURLPARK:
1) Face - Easiest read out of expression including emotion.
2) Body - Encapsulation of all organs, systems, the mind, and wearables as one body.
3) Home - Both the location, capability, and function to serve as a base for daily living.  Can include any location you would stay at.
4) Landscape - Areas you visit that hold biomes or networks of life between species.
5) Sea, Space, and Spaceships - Frontiers between places.
6) Cities - Interaction of work places, resource structures, homes, and individual bodies representing a biome cluster including neighborhoods.
7) Artifacts - Any object we can find, wear, or trade.
8) UI and Deployment mechanism to allow sharing and interactivity with no code applications and services.




# Ganbreeder

[Ganbreeder](https://ganbreeder.app) is a collaborative art tool for discovering images. Images are 'bred' by having children, mixing with other images and being shared via their URL. This is an experiment in using breeding + sharing as methods of exploring high complexity spaces. GAN's are simply the engine enabling this. Ganbreeder is very similar to, and named after, Picbreeder. It is also inspired by an earlier project of mine [Facebook Graffiti](http://www.joelsimon.net/facebook-graffiti.html) which demonstrated the creative capacity of crowds.Ganbreeder uses [these](https://tfhub.dev/deepmind/biggan-128/2) models.

This code was made in a weekend and hasn't been cleaned up or documented yet. There are also improvements to make to scalability.

Pull request are more than welcome :)

## How to use

### Prerequisites
* Install Python 3 + pip (for the GAN server)
* Install NodeJS + npm (for the frontend)
* Install a PostgreSQL server

### Launch the GAN server
```bash
cd gan_server
# Install dependencies
pip install -r requirements.txt
# And go...
python server.py
```
Your GAN server is available at http://localhost:5000/

### Configure the frontend
For quick hacking, if you have Docker at your disposal, you can spawn a PostgreSQL database like so:
```bash
docker run -p 5432:5432 --name ganbreederpostgres -e POSTGRES_PASSWORD=ganbreederpostgres -d postgres
```
With that simple scenario, the database and user would be `postgres` and the password would be `ganbreederpostgres`

Copy the file `server/example_secrets.js` to `secrets.js` and modify it to fit your environment.

### Launch the frontend
```bash
cd server
npm install
# Create the database structure
node_modules/knex/bin/cli.js migrate:latest
# Generate the first images
node make_randoms.js
# Generate a cache of image keys for the front page (do it every time you want to update the front page)
node updatecache.js
# And go...
node server.js
```
Your frontend is available at http://localhost:8888/

### docker-compose setup

Make sure that [docker](https://docs.docker.com/install/) and [docker-compose](https://docs.docker.com/compose/install/) are installed.

Start the containers:
```bash
docker-compose up
```
Your frontend is available at http://localhost:8888/, backend at http://localhost:5000/.
Initial backend setup can take few minutes.

If this is the first time you are running the project you might want to generate some random images:
```bash
docker-compose exec server node make_randoms.js
```
Restart only frontend server (to avoid backend initialization wait):
```bash
docker-compose restart server
```
