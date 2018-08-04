##############################################################################
####################### Quest do Selo Megingjard ###############################
##############################################################################
#Pre-requisitos:
# - Deixar salvo em prontera
# - Deixar 3 asas de borboleta
# - Deixar pelo menos 150k zenny
# - Deixar itens da quest na kafra (Verificar se os itens da quest que pega na kafra são os que estão na macro)
# - Ter no inventário Prontera Warp Pass
##############################################################################
#Configurações adicionais no kore para reconhecimento do Prontera Warp Pass
# Na pasta table/iRO adicionar nos arquivos:
# Arquivo: items-custom - add a linha: 19662#Prontera_Warp_Pass#
# Arquivo: itemsdescriptions-custom - add a linha: 19662#Prontera Warp Pass#
##############################################################################
#Ativa digitando: macro selomegingjard
##############################################################################

macro selomegingjard {
	do conf route_randomWalk 0
	do conf attackAuto 0
	do conf attackAuto_party 0
	do conf itemsTakeAuto 0
	do conf autoTalkCont 0
	call storage
}

macro storage {
	do is Prontera Warp Pass
	pause 2
	do move prontera 142 94
	pause 2
	do talknpc 146 89 c r0
	pause 5
	do storage get Slick Paper 2
	do storage get Oil Paper 1
	do storage get Squid Ink 3
	do storage get Bird Feather 3
	do storage get Blue Gemstone 20
	do storage get Alcohol 2
	do storage get Magnifier 5
	do storage get Green Herb 1
	do storage get Poring Doll 1
	pause 3
	do storage close
	pause 5
	call Rebarev_Doug
}

#Rebarev Doug
macro Rebarev_Doug {
	do move prt_castle 42 150
	pause 5
	do talknpc 44 151 c c c c c c c c c r0 c c r0 c c c c c c n
	pause 5
	do talknpc 44 151 c c r1 n
	pause 5
	call Librarian
}

#Librarian Jekan
macro Librarian {
	do move prt_in 175 103
	pause 5
	do talknpc 172 106 c c c c r3 c t="the 1st squad's final mission" c n
	pause 5
	call Rebarev_Doug2
}

#If these steps do not work and the reply is "maybe yes maybe no", try returning to Rebarev Doug in the castle and repeat until the third option is obtained.
#Tem que ir falando com ele ate aparecer uma terceira opcao. Nao sei como desenvolver algo que assim ele ativar a opcao, siga os passos abaixo.
macro Rebarev_Doug2 {
	do move prt_castle 42 150
	pause 5
	do talknpc 44 151 c c r2 c c c c c c n
	pause 5
	call Librarian2
}

macro Librarian2 {
	do move prt_in 175 103
	pause 5
	do talknpc 172 106 c c c c c r3 c t="the 1st squad's final mission" c n
	pause 3
	do talk resp 2
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk resp 0
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk resp 1
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 5
	call Librarian3
}

macro Librarian3 {
	do talknpc 172 106 c c c c c r2 c c r0 c r1 c n
	pause 5
	do move prt_in 168 106
	pause 5
	call 
}
	
#Tem 5 npc na prateleira de livros e tem que falar com eles ate achar: The 3rd Platoon Records
#Tem que abrir com o Open Kore para selecionar esse npc.
# A File#megin1 (172, 109) -> Encontrei nesse o The 3rd Platoon Records na primeira vez.
# A File#megin2 (170, 109) -> Encontrei nesse o The 3rd Platoon Records na terceira vez.
# A File#megin3 (168, 109) -> Encontrei nesse o The 3rd Platoon Records na quarta vez.
# A File#megin4 (169, 109)
# A File#megin5 (166, 109) -> Encontrei nesse o The 3rd Platoon Records na segunda vez.

do talknpc 172 109
do talknpc 170 109
do talknpc 168 109
do talknpc 169 109
do talknpc 166 109

#A File#megin2: You have found The 3rd Platoon Records!
#Apareceu a msg acima, creio que tera que criar um automacro para ir procurando nos arquivos.
#Quando encontrar vai para a proxima etapa

macro Librarian4 {
	do talknpc 172 106 c c r0 c c c c c c n
	pause 5
	call Librarian5
}

macro Librarian5 {
	do talknpc 172 106 c c n
	pause 5
	call Librarian6
}

#Tem que ir clicando nele ate habilitar conversa.
#Essa é o log que mostra quando vc tenta habilitar a conversa:
#Librarian#megin: [Librarian Jekan]
#Librarian#megin: Let me go over and review the document before I make a copy...
#NPC Librarian#megin (7): Conversa Finalizada.
#Essa é o log que mostra quando vc habilitar a conversa:
#Librarian#megin: [Librarian Jekan]
#Librarian#megin: There you go. As I thought, the document didn't seem to contain any crucially important data.
#Librarian#megin: [Librarian Jekan]
#Librarian#megin: Just remember, this copy needs to stay in the Prontera Library. That means you have to come back if you need to read the document again.
#NPC Librarian#megin (7): Conversa Finalizada.

macro Librarian6 {
	do talknpc 172 106 c n
	pause 5
	call librarian7
}

macro librarian7 {
	do talknpc 172 106 c r0 c t="crusader 3rd_company 3rd_platoon 1st_squad record"
	pause 3
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk cont
	pause 2
	do talk resp 4
	pause 2
	call Zan_Huadoku
}

#Zan Huadoku
macro Zan_Huadoku {
	do is Prontera Warp Pass
	pause 2
	do move geffen_in 105 163
	pause 5
	do talknpc 109 161 c c c r0 c c c c c c c c n
	pause 5
	do talknpc 109 161 c c c r2 c c c c c c c c c c n
	pause 5
	call Zan_Huadoku2
}

#Keep talking to this NPC until he speaks about the unknown fragment. After that, talk to him again until he repeats himself.
macro Zan_Huadoku2 {
	do talknpc 109 161 c c c c c c n
	pause 10
	call Zan_Huadoku3
}

macro Zan_Huadoku3 {
	do talknpc 109 161 c n
	pause 5
	call Inn_Employee
}

#Inn Employee
macro Inn_Employee {
	do is Prontera Warp Pass
	pause 5
	do move morocc_in 142 139
	pause 5
	do talknpc 147 141 c r0 n
	pause 5
	call Inn_Employee2
}

#Se ele te matar, precisa repetir essa parte ate mudar para a fala abaixo.
#Select any of the options until you receive a clue that says "Aragham never hoarded upgrade items."
macro Inn_Employee2 {
	do move morocc_in 143 176
	pause 5
	do talknpc 146 179 c c t="Donon" c c c r0 c c c
	pause 5
	call Inn_Employee3
}

#Select any of the options until you receive a clue that says "Aragham never hoarded upgrade items."
macro Inn_Employee3 {
	do talknpc 146 179 c c n
	pause 5
	call prontera
}

#Salvar em prontera
macro prontera {
	do is Prontera Warp Pass
	pause 5
	do move prontera 142 94
	pause 5
	do talknpc 146 89 c r1 n
	pause 5
	call warpcmd_field09
}

#Ele precisa ir para cmd_fild09. Sugiro deixar um priest/monk para dar warp quando o char do selo enviar algum comando.
#Usar o Champ dessa conta: zica171 / 171731

#Fortress Saint Darmain
macro warpcmd_field09 {
	do move prontera 208 92
	pause 5
#Aqui criar o comando para mandar pm e abrir warp para cmd_fild09.
	call 
}

macro portal {
	do move cmd_fild09 106 194
	pause 5
	do talk cont
	pause 2
	do talk resp 1
	pause 2
	do talk resp 2
	pause 2
	do talk resp 1
	pause 2
	do talk resp 0
	pause 2
	do talk cont
	pause 2
	call Suspicious_Man
}

#Suspicious_Man
macro Suspicious_Man {
	do move in_rogue 243 57
	pause 5
	do talknpc 243 61 c c c c r1 c c c c n
	pause 5
	do talknpc 243 61 c c c c r0 c c c c c c c c c c c c c c c n
	pause 5
#confirmar se essa parte deu certo. para confirmar, verificar se ira falar com o proximo npc
	do talknpc 243 61 c c c c r2 c c r2 n
	pause 5
}



