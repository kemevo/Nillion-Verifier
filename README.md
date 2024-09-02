# Nillion-Verifier

# Telegram
- https://t.me/HerculesNode

## System requirements
 - Ubuntu 22.04+
 - 2-4 GB RAM
 - 2+ vCPUs
 - 50 GB storage
- [Resmi kaynak](https://nillion.com/news/1007/)

## Faucetten token temini
>Burdan keplr cüzdanına ağı eklioruz: https://chains.keplr.app/

>Daha sonra kepler cüzdanında, sol üstten "Settings" kısmına gelip, "Manage Chain Visibility" kısmından nillion açıyoruz. Artık ağ gözüktüğüne göre adresinizi kopyalayabilirsiniz.

>Burdan test token temin ediyoruz: https://faucet.testnet.nillion.com/

## Node Kurulumu
### Her satırı tek tek kopyalayıp, çalıştıralım.
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git make curl screen tar wget jq build-essential -y 
sudo apt install make clang pkg-config libssl-dev -y
curl -fssl https://get.docker.com | bash -s docker
docker pull nillion/retailtoken-accuser:v1.0.0
cd
mkdir -p nillion/accuser
docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 initialise
```

### Log çıktısında account_id ve public key kaydediyoruz.

## Portal Kaydı
> Buraya girip, verifier tıklıyoruz. Bilgileri dolduruyoruz: https://verifier.nillion.com/

## Faucetten token temini - 2
> Burdan loglarda çıktı olarak gözüken adrese test token temin ediyoruz: https://faucet.testnet.nillion.com/

> [!CAUTION]
> Bu aşamadan sonra 30-60 dk bekliyoruz.

## Node çalıştırma (sondaki block height kısmı resmi siteden alın)
```bash
docker run -d --name nillion_node -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "https://testnet-nillion-rpc.lavenderfive.com" --block-start 5266535
```
>Loglara bakma (Registered: true yazması gerekiyor)
```
docker logs -f nillion_node --tail 50
```
> Alternatif RPC'ler:
```
https://testnet-nillion-rpc.lavenderfive.com
https://nillion-testnet-rpc.polkachu.com
```

## Registered: False hatası alanlar
> İlk önce https://verifier.nillion.com/ burdan tekrar verify yapmayı deneyin olmazsa aşağıdaki adımları deneyin farklı rpc ile.  (sondaki block height kısmı resmi siteden alın)

```bash
docker stop nillion_node
docker rm nillion_node
docker run -d --name nillion_node -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:v1.0.0 accuse --rpc-endpoint "FARKLI RPC BURAYA" --block-start 5266535
```

## Secrets kısmı görevleri
> 1. Görev avcunuzun resmini yükleyin.
> 2. Görev keplr adresinizi kaydedin.


