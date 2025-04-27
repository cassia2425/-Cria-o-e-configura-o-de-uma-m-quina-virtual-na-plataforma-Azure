# Cria o e configura o de uma maquina virtual na plataforma Azure
  Criação de Maquinas Virtuais no Microsoft Azure
  
   # INTRODUÇÃO
   
Criar máquinas virtuais no Microsoft Azure pode parecer uma tarefa complicada, mas com este guia passo a passo, você verá que é mais simples do que parece. Vamos explorar a criação de máquinas virtuais tanto para Linux quanto para Windows. Vamos começar!

# Passo 1: Criação do Resource Group

Antes de criar qualquer recurso no Azure, precisamos de um Resource Group, que funciona como um contêiner lógico para todos os recursos relacionados. Vamos criar um Resource Group chamado rg-example.

#### 1. Acesse o portal do Azure.
#### 2. Vá para “Resource Groups” e clique em “Create”.
#### 3. Nomeie seu Resource Group como rg-example.
#### 4. Selecione a região desejada.
#### 5. Clique em “Review + Create” e, em seguida, “Create”.

![Captura de tela 2025-04-27 10155401](https://github.com/user-attachments/assets/557d2263-7f91-42d9-8fcb-ee02d9bdc8ec)

# Passo 2: Criação da Virtual Network
A próxima etapa é criar uma Virtual Network (VNet), que permite a comunicação entre recursos do Azure.

#### 1. Vá para “Virtual Networks” e clique em “Create”.
#### 2. Nomeie a VNet como vnet-example.
#### 3. Selecione o Resource Group rg-example.
#### 4. Configure o endereço IP e as sub-redes conforme necessário.
#### 5. Clique em “Review + Create” e, em seguida, “Create”.

![Captura de tela 2025-04-27 10195402](https://github.com/user-attachments/assets/b04af0a3-a416-41bc-b4db-b9eaa8a96b6e)

# Passo 3: Criação da NSG (Network Security Group)

O Network Security Group (NSG) é responsável por controlar o tráfego de rede para as VMs. Vamos criar um NSG chamado nsg-example.

#### 1. Vá para “Network Security Groups” e clique em “Create”.
#### 2. Nomeie o NSG como nsg-example.
#### 3. Selecione o Resource Group rg-example.
#### 4. Clique em “Review + Create” e, em seguida, “Create”.

  # Creart virtual network
  
![Captura de tela 2025-04-27 103343](https://github.com/user-attachments/assets/b75a25bd-74d4-4358-8f0e-f857770ad7c0)


# Passo 4: Anexar o NSG à Subnet

### Depois de criar o NSG, precisamos anexá-lo à Subnet default da nossa VNet vnet-example.

#### 1. Acesse o NSG nsg-example e selecione a settings > Subnet.
#### 2. Associate, selecione a subnet default e salve as alterações.

![Captura de tela 2025-04-27 10383104](https://github.com/user-attachments/assets/cb95f37e-1896-4cb6-bf1e-e54dbee58d58)

# Passo 5: Criação da Virtual Machine Linux

### Vamos criar a VM com nome vm-example dentro do rg-example com o tipo de segurança: Standard.


![05](https://github.com/user-attachments/assets/53022daf-ee41-4661-b41c-c574d9e70f13)]

#### 1. Vá para “Virtual Machines” e clique em “Create”.
#### 2. Selecione o Resource Group rg-example.
#### 3. Nomeie a VM como vm-example.
#### 4. Altere o tipo de segurança para Standard.
#### 5. Selecione “Ubuntu Server 20.04 LTS ARM64 Gen2” como a imagem.
#### 6. Selecione “Arm64” como a arquitetura (para maior eficiência energética e de processamento).
#### 7. Configure a VM com o tamanho Standard_D2ps_v5.
#### 8. Escolha a autenticação por senha e defina uma senha.
#### 9. Certifique-se de que a VM não tenha portas de entrada públicas configuradas.

![06](https://github.com/user-attachments/assets/6513258f-0315-4580-be27-cb4ba64fa5d3)

#### 1. Na seção “Networking”, certifique-se de que a VM esteja na VNet vnet-example e na Subnet default.
#### 2. Selecione “Review + Create” e, em seguida, “Create”.


![example6](https://github.com/user-attachments/assets/ba513ca1-f94e-4fdd-bb64-11764d50fadb)


## Após a criação, precisamos liberar a porta SSH 22 no NSG nsg-example para acessar a VM.

#### 1. Acesse o NSG nsg-example.
#### 2. Adicione uma regra de entrada para permitir o tráfego na porta 22.

![example7](https://github.com/user-attachments/assets/88750e47-f3ab-4dd2-9466-46ed6dcf78b5)

## Conectando-se à VM Linux

#####  Após a VM estar em execução verifique qual IP público foi atribuído à VM , copie o IP público e conecte-se via SSH:

##### ssh usuario@IPX.XXX.XXX.XX

### No meu caso:
#### ssh raafel@172.210.28.194

![example8](https://github.com/user-attachments/assets/dcae61de-9493-41fd-888a-eb476d638205)

 
## Criação da Virtual Machine Windows 11

Vamos criar uma VM com Windows 11 dentro do nosso rg-example, com o nome vm-example-win, tipo de segurança Standard e imagem Windows 11 Pro.

#### 1. Vá para “Virtual Machines” e clique em “Create”.
#### 2. Selecione o Resource Group rg-example.
#### 3. Nomeie a VM como vm-example-win.
#### 4. Altere o tipo de segurança para Standard.
#### 5. Selecione “Windows 11 Pro” como a imagem.

![example13](https://github.com/user-attachments/assets/9bca1483-85ba-4cf5-99dd-6f6aec5a6f0d)

#### 1. Configure a VM com o tamanho Standard_B4ms para testes mais rápidos.
#### 2. Escolha a autenticação por senha e defina uma senha de sua preferência (não se esqueça de anotar a senha).
#### 3. Certifique-se de que a VM não tenha portas de entrada públicas configuradas. Confirme a licença.




![example14](https://github.com/user-attachments/assets/f65ba0c3-b4b3-453e-8a94-85e493af83a0)

#### 1. Na seção “Networking”, certifique-se de que a VM esteja na VNet vnet-example e na Subnet default, e que não seja atribuído um NSG à NIC.
#### 2. Selecione “Review + Create” e, em seguida, “Create”.

![example15](https://github.com/user-attachments/assets/ab11d7f3-ea3a-49ac-856a-1d809a6e6285)

#### Após a criação, precisamos liberar a porta RDP no NSG nsg-example para acessar a VM.

#### 1. Acesse o NSG nsg-example.
#### 2. Adicione uma regra de entrada para permitir o tráfego na porta RDP.


![example16](https://github.com/user-attachments/assets/a73f0db6-0c46-4855-9dd8-40d6f93eea77)


# Conectando-se à VM Windows
#### 1. No seu computador com Windows, abra o aplicativo “Remote Desktop Connection” (procure por “Remote” no menu Iniciar).


![example22](https://github.com/user-attachments/assets/68bdafe1-dacb-46de-8769-53c6d627134e)


### Copie o IP público atribuído à VM vm-example-win, digite no Remote Desktop Connection, clique no botão conectar, escolha “Use another account”, e digite o usuário e senha que foram criados anteriormente. Clique em “OK”.



![example17](https://github.com/user-attachments/assets/e30a2ebf-c366-489a-8b09-250454820fdf)

### Confirme o certificado de segurança quando solicitado:


![example18](https://github.com/user-attachments/assets/11406c9b-c6f7-451e-ac90-2a01dc5f40df)

# Conclusão

Criar máquinas virtuais no Azure é um processo estruturado que envolve a criação de vários componentes, como Resource Groups, Virtual Networks e Network Security Groups. Seguindo este guia, você pode configurar rapidamente VMs Linux e Windows para atender às suas necessidades. Lembre-se de sempre garantir a segurança das suas VMs e otimizar suas configurações para o melhor desempenho.

A flexibilidade e o poder do Azure permitem que você adapte a infraestrutura de TI às demandas específicas do seu projeto, seja ele para desenvolvimento, teste ou produção. Utilize as práticas recomendadas para maximizar a eficiência e a segurança de suas VMs.

