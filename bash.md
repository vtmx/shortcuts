# Bash

## Variáveis
| Variável | Descrição
| --- | --- |
| $? | Recebe última saída recebida |
| $$ | Descrever |
| !! | Exibe o último comando |
| $_ | Pega último parâmetro passado |
| $* | Todas as expansões unificadas |
| $@ | Todas as expansões |
| $0 | Exibe shell atual |
| $BASHPID | Exibe o ID do bash |
| $BASHREMATCH | Retorna o último padrão criado |
| $CDPATH | |
| $PIPESTATUS[@] | |
| $PROMPT_COMMAND | Executa o conteúdo antes de devolver ao prompt |
| $RANDOM | Gera número aleatório $((RANDOM%6+1)) dado |
| $REPLY | Conteúdo do último campo válido |
| $OLDPWD | Último diretório visitado echo ~- mesmo resultado ~+ igual PWD |
| $SHLVL | Exibe a atual instância do shell |

```bash
# Comparar se está ou não em um subshell
$$ vs $BASHPID

# Repete o mesmo comando anterior do usuário
sudo !!

# Cria um arquivo novo ou excluí o conteúdo de um existente
ls >teste.txt

# Adiciona texto no início da linha do arquivo
echo "$(echo Meu texto; cat file)" > file
text=$(cat - nums <<< 'I P'); echo "$text" > nums
echo I P | cat /dev/stdin -
cat - nums <<< 'I P' | tee nums
sed -i '1i I P' nums
echo "$(cat - nums <<< 'I P')" > nums

# Diretório de execução
script_dir=${0%/*}

# Verifica se programa existe
type firefox
echo $?

# Habilita opções
# Ativa e desativa opção
shopt -s extglob

# Exibe a opção se está ativa ou não
extglob

# Adiciona o conteúdo em algum arquivo existente
ls >>teste.txt

# Redirecionamento
teste < arquivo

cat << eof
teste
eof

grep 'teste' <<< 'teste'

# Executa o segundo enquanto o primeiro ainda está em execução
comando1 & comando2

# Executa o segundo comando caso o primeiro seja ok
comando1 && comando2

# Repete var
echo ${var}{,}
vida vida
echo ${var}{,,,}
vida vida vida vida

# Executa o segundo caso o primeiro falhe
comando1 || comando2

# Expandi variável
var="banana laranja"
ctrl+alt+e = expandi as variáveis no terminal

# Executa o segundo sem está em uma nova linha
comando1; comando2

# Recebe argumento de entrada
local entrada1=$1
local entrada2=$2

# Recebe valor de entrada
read -rp "Digite um valor: " nome_var

# Testa saída do comando
if ls; then
  echo "comando executado com sucesso"
else
  echo "comando terminado com falha"
fi

# Oculta qualquer tipo de erro
comando &>/dev/null

# Descobrir variável PS1
printf "%q\n" "$PS1"

# Ligar e desligar opções
# Ligar
shopt -s globasciiranges

# Ligar
shopt -u globasciiranges

# Parâmetros expansão
$0 $1 $2 $3 $4 $5 $6 $7 $8 $9
# Repetindo parâmetros
echo {left,right}{,}
echo go_to {left,right,up,down}{,,,}

# Tranca a saída de erro, mais rápido que /dev/null
ls -la  2>&-

# Exemplo imagem do kernel
url='https://www.kernel.org'
while read; do
    wget -O /tmp/${REPLY##*/} "$url/$REPLY"
done < <(wget -qO- "$url"|grep -oP 'src="\K.*(png|jpg)(?=")')

# Declara variáveis inteiras 
declare -i a+=b
let a+=b

# Renomear múltiplas extednções
for file in *.json; do
  mv "$file" "${file%.json}.yml"
done

# Receber resultado do grap em array
readarray ids <<< $(grep -Eo '<Id>[[:digit:]]*</Id> file.xml)

# Algumas vezes fica com um espaço a mais, para solucionar use o argumento -t
readarray -t components_files <<< "$(ls ${components_dir}/*.html)"

# Somar valor em xml
sed -E "s|<Id>([[:digit:]])*)echo "</Id>|<Id>$((\1 + 2))</Id>"|ge

# Rename pattern
for file in pattern_*;
  do mv "$file" "${file//*_/}";
done

# Debug
set -x
...code debug...
set +x

# Alinhando texto
column -t arq.csv 

# Exibe arquivo formatado com 60 colunas
fold -sw 60 arq.txt

# Curl install
curl -sSL https://get.docker.com/ | sh
sh -c "$(curl -sSL https://get.docker.com/)"

# App exist
if type firefox2 >& /dev/null; then  
  echo Firefox existe
else
  echo Firefox não existe
fi

# Ir para a parte final do arquivo
less +F arq

# Exibe texto com marcas de nova linha
cat -et

# Converter PascalCase para kebab-case

# 1
sed -E 's/([A-Z])/-\1/2g' <<< 'PalavraCruzadaAlinhada' | tr [[:upper:]] [[:lower:]]

# 2
converter_para_hifen() {
    local palavra="$1"
    palavra_convertida="${palavra//[A-Z]/-&}"
    palavra_convertida="${palavra_convertida,,}"
    palavra_convertida="${palavra_convertida#-}"
    echo "$palavra_convertida"
}

entrada="$1"
saida=$(converter_para_hifen "$entrada")
echo "$saida"

# 3
foo="TestPascalCaseString"
while [[ "$foo" =~ (.*[a-z0-9])([A-Z].*) ]] && foo="${BASH_REMATCH[1]}-${BASH_REMATCH[2]}"; do
  :  # do nothing
done
echo "${foo,,}"

# Exemplo exercício
grep -E -A1 '^(Country|City|Bairro)$' <<< "$var" | paste - - | awk '{print $1 "\t-\t" $2}'
```
