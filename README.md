# Scallop Summer School (Salem, MA 2024)

## Setup
To run the docker container (build takes around ~20 min):
```
docker build -t scallop-summer24-tutorial -f x86_64/Dockerfile .
docker run -it --name scallop-summer scallop-summer24-tutorial
```
After this, you should see the following prompt:
```
(base) root@c36cbd85bb7b:~/labs$
```
Be sure to activate the conda environment with:
```
conda activate scallop-env
```
To use OpenAI features, add the following line to the container's `~/.bashrc`:
```bash
export OPENAI_API_KEY="<YOUR_OPENAI_KEY>"
```