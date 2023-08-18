<p align="center">
  <img height="100" height="auto" src="https://github.com/freshe4qa/kroma/assets/85982863/939c377b-b0bf-4805-a6f4-6b5a03a4b046">
</p>

# Kroma Testnet

Official documentation:
>- [Validator setup instructions](https://docs.kroma.network/developers/running-nodes-on-kroma)

Explorer:
>- [Sepolia Explorer](https://sepolia.etherscan.io/)
>- [Kroma Explorer](https://blockscout.sepolia.kroma.network/)

### Minimum Hardware Requirements
 - 2+ CPUs;
 - 4GB+ RAM
 - 200GB+ (SSD or NVME)
 - Ubuntu 20.04

## Установка
```
sudo apt update
sudo apt install git ca-certificates curl gnupg unzip wget -y    
```

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

```
sudo install -m 0755 -d /etc/apt/keyrings
sudo rm -f /etc/apt/keyrings/docker.gpg
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

```
cd $HOME && mv kroma-up kroma-up_$(date +%s) 2>/dev/null
git clone https://github.com/kroma-network/kroma-up.git
cd kroma-up && ./startup.sh
```

Используем [Alchemy](https://alchemy.com/?r=zcwMjU5NDc4ODI3O) или любой другой провайдер RPC, берем оттуда Sepolia Testnet: Https 
```
nano .env
```

- В поле L1_RPC_ENDPOINT вставляем вашу ссылку https
- В поле KROMA_VALIDATOR__PRIVATE_KEY вставляем ваш приватный ключ Metamask.

После того как все сделали в терминале кликаем CTRL+O, затем Enter, затем CTRL+X, чтобы выйти.

Обратите внимания на то, чтобы внести депозит в валидатор пул нужно чуть больше 1 эфира в сети Sepolia Testnet.

Запускаем ноду
```
docker compose --profile validator up -d
./sync_block.sh
```

Просмотр логов
```
cd $HOME/kroma-up
docker compose --profile validator logs -f
```

Депозит в пул
```
docker exec kroma-validator kroma-validator deposit --amount 1000000000000000000
```
