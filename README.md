# Weather Monitoring System

## Objective

The Weather Monitoring System is a real-time data processing application that continuously monitors weather conditions for major metros in India. The system retrieves data from the [OpenWeatherMap API](https://openweathermap.org/) and provides summarized insights using rollups and aggregates.

## Data Source

The system utilizes the OpenWeatherMap API to retrieve various weather parameters, focusing on:
- **Main**: Main weather condition (e.g., Rain, Snow, Clear)
- **Temp**: Current temperature in Centigrade
- **Feels Like**: Perceived temperature in Centigrade
- **DT**: Time of the data update (Unix timestamp)

## Features

### Real-Time Data Processing
- The system continuously calls the OpenWeatherMap API at a configurable interval (e.g., every 5 minutes) to fetch weather data for the following metros in India:
  - Delhi
  - Mumbai
  - Chennai
  - Bangalore
  - Kolkata
  - Hyderabad

### Rollups and Aggregates

1. **Daily Weather Summary**
   - Roll up weather data for each day.
   - Calculate daily aggregates for:
     - Average temperature
     - Maximum temperature
     - Minimum temperature
     - Dominant weather condition (determined by the most frequent weather type during the day).

2. **Alerting Thresholds**
   - User-configurable thresholds for temperature or specific weather conditions.
   - Continuous tracking of the latest weather data to compare against thresholds.
   - Alerts triggered if thresholds are breached (e.g., temperature exceeds 35°C for two consecutive updates).

3. **Visualizations**
   - Display daily weather summaries, historical trends, and triggered alerts.

## Technology Stack

- **Django**: A high-level Python web framework that enables rapid development and clean, pragmatic design.
- **Celery**: An asynchronous task queue/job queue used for handling background tasks, allowing efficient execution of the weather data retrieval process.
- **Redis**: An in-memory data structure store that acts as a message broker for Celery, ensuring fast communication between the application and worker processes.
- **Requests**: A simple HTTP library for Python, used for making API calls to the OpenWeatherMap API to retrieve weather data.
- **python-dotenv**: A library to read key-value pairs from a `.env` file and set them as environment variables, making it easier to manage sensitive information like API keys.
- **Matplotlib**: A plotting library for Python that is used for creating static, interactive, and animated visualizations of the weather data.
- **Docker**: A containerization platform to package the application and its dependencies into a container for easy deployment and scalability.

## Installation

### Prerequisites
- **Python 3.x** installed on your system.
- **Redis** installed and running on your system.
- **Docker** and **Docker Compose** installed.

### Installation Steps

1. **Clone the repository**:
   ```bash
   git clone https://github.com/pranav824/Assignment2_Pranav.git

2. **Install the dependencies in the requirement.txt file**

3. **Install redis in the local system**

4. **Dockerize the application by running the following commands**
   To create docker file:
   New-Item -Path . -Name "Dockerfile" -ItemType "file"

   Create a .dockerignorefile:
   New-Item -Path . -Name ".dockerignore" -ItemType "file"

   Create a docker-compose.yml (Optional):
   New-Item -Path . -Name "docker-compose.yml" -ItemType "file"
   
   Build the Docker Image:
   docker build -t django-app .
   
   Run the Docker Container:
   docker-compose up

5. **Execute the following commands before running the server**

   celery -A weather_monitoring worker --pool=solo --loglevel=info (celery worker: Executes tasks that have been sent to the queue.)
   celery -A weather_monitoring beat --loglevel=info (celery beat: Schedules tasks to be sent to the queue periodically based on a schedule you define.)

6. **Run Server**
   
   python manage.py runserver

**Note** : As a best practice I have used virtual environment here. Kindly define a new venv in your system and follow up the procedure mentioned above or run the cloned application globally in your system after installing dependencies in the requirements.txt file.
   
   
