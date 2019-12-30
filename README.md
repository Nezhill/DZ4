#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <string.h>


void Find(char **table, int amount, char arrow[3]){
    int degree[amount], min_degree = 256;
    
    for(int i=0 ;i<amount; i++){//РїРѕРґСЃС‡РµС‚ СЃС‚РµРїРµРЅРё РІРµСЂС€РёРЅС‹
        degree[i] = 0;
        for(int j=0; j<amount; j++){//СЃРѕР±СЃС‚РІРµРЅРЅРѕ РѕРЅ СЃР°РјС‹Р№
            degree[i] += table[i][j+1];
            degree[i] += table[j][i+1];
        }
        if(min_degree > degree[i]){//РЅР°С…РѕРґРёРј РјРёРЅРёРјР°Р»СЊРЅСѓСЋ РІРµСЂС€РёРЅСѓ
            min_degree = degree[i];
        }
    }
    
    printf("\nРІСЃРµ СЂРµР±СЂР° СЃ РјРёРЅРёРјР°Р»СЊРЅРѕР№ РІРµСЂС€РёРЅРѕР№ = %d:\n",min_degree);
    for(int addr=0; addr < amount; addr++){//РїСЂРѕС…РѕРґРёС‚ РїРѕ СЃС‚СЂРѕРєР°Рј 
        if(degree[addr] == min_degree){//РїСЂРѕРІРµСЂРєР° СЏРІР»СЏРµС‚СЃСЏ Р»Рё РґР°РЅРЅР°СЏ РІРµСЂС€РёРЅР° РІРµСЂС€РёРЅРѕР№ СЃ РјРёРЅ СЃС‚РµРїРµРЅСЊСЋ  
            for(int i=0; i<amount; i++)//РїСЂРѕС…РѕРґРёС‚ РїРѕ СЃС‚РѕР»Р±С†Р°Рј
                if( table[addr][i+1] > 0)//РїСЂРѕРІРµСЂРєР° РЅР° РЅР°Р»РёС‡РёРµ РІ СЏС‡РµР№РєРё Р·Р°РїРёСЃРё Р±РѕР»СЊС€Рµ 0
                    for(int j=0; j<table[addr][i+1]; j++)// РµСЃР»Рё РІ СЏС‡РµР№РєРµ Р±РѕР»СЊС€Рµ С‡РµРј 1 РІС‹РІРѕРґРёС‚ Р±РѕР»СЊС€Рµ С‚Р°РєРёС… Р·Р°РїРёСЃРµР№
                        printf("%c%s%c; ", table[addr][0], arrow, table[i][0]);

            for( int i=0; i<amount; i++ )//С‚Р° Р¶Рµ СЃР°РјР°СЏ С‚РѕР»СЊРєРѕ РЅР°РѕР±РѕСЂРѕС‚ 
                if( table[i][addr+1] > 0 && addr != i && degree[i] != min_degree)
                    for( int j=0; j<table[i][addr+1]; j++ )
                        printf("%c%s%c; ", table[i][0], arrow, table[addr][0]);
        }
    }
    printf("\n");
}



int main(){
    int mode;
    printf("Р’РІРµРґРёС‚Рµ 0 РґР»СЏ РѕСЂРёРµРЅС‚РёСЂРѕРІР°РЅРЅРѕРіРѕ РіСЂР°С„Р° \nРёР»Рё 1 РґР»СЏ РЅРµРѕСЂРёРµРЅС‚РёСЂРѕРІР°РЅРЅРѕРіРѕ\n\n");
    scanf("%d", &mode);
    
    if(!( mode == 1 || mode == 0 ))
        exit(101);
    
    printf("Р’РІРµРґРёС‚Рµ РєРѕР»РёС‡РµСЃС‚РІРѕ РІРµСЂС€РёРЅ::\n> ");
    int amount;
    scanf("%d",&amount);
    if (amount <= 0){
        printf("РќРµ РїРѕР№РґРµС‚, РґР°РІР°Р№ РїРѕ РЅРѕРІРѕР№\n");
        exit(102);
    }
    
    getchar(); // Р±РµР· РЅРµРіРѕ РЅРµ СЂР°Р±РѕС‚Р°РёС‚. РїСЂРѕРїСѓСЃРєР°Рµ /n
    printf("РќР°Р·РІР°РЅРёРµ РІРµСЂС€РёС€\n");
    
    char **table; //СѓРєР°Р·Р°С‚РµР»СЊ РЅР° СѓРєР°Р·Р°С‚РµР»СЊ С‚Рє РґРІРѕР№РЅРѕР№ РјР°СЃСЃРёРІ
    table = calloc(amount, sizeof(char*));// С‚Рє РјР°СЃСЃРёРІ 2-РѕР№ 
    for(int i=0; i<amount; i++){
        table[i] = calloc(amount+1, sizeof(char));
    }
    
    for(int i=0; i<amount; i++){
        printf("%d: ",i);
        table[i][0] = getchar(); // РїРѕ РЅР°Р·РІР°РЅРёСЋ
        getchar(); //РїСЂРѕРїСѓСЃРєР°РµС‚ СЃР»СЌС‰ СЌРЅ

        if(!(('A' <= table[i][0] && table[i][0] <= 'Z') || ('a' <= table[i][0] && table[i][0] <= 'z'))){
            printf("Р’РІРµРґРёС‚Рµ Р±СѓРєРІСѓ!\n");// РїСЂРѕРІРµСЂСЏРµС‚ С‡С‚РѕР±С‹ Р±С‹Р»Рё Р±СѓРєРІС‹
            i--; // -- РµСЃР»Рё РѕС€РёР±РєР°
        } else {
            for(int j=0; j<i; j++){
                if( table[i][0] == table[j][0] ){ // РµСЃР»Рё СЃРѕРІРїР°РґР°СЋС‚ Р±СѓРєРІС‹
                    printf("Р’РІРµРґРёС‚Рµ РґСЂСѓРіСѓСЋ Р±СѓРєРІСѓ\n");
                    i--;
                }
            }
        }
    }
        
    for(int i=0; i<amount; i++){
        for(int j=1; j<amount; j++){
            table[i][j] = 0; // РѕР±РЅСѓР»РµРЅРёРµ РІСЃРµРіРѕ РєСЂРѕРјРµ Р±СѓРєРІ
        }
    }
    
    printf("Р”Р»СЏ РєР°Р¶РґРѕР№ РІРµСЂС€РёРЅС‹ РІРІРµРґРёС‚Рµ СЃРІСЏР·СЊ\n");
    for(int i=0; i<amount; i++){
        printf("%c -> ", table[i][0]);
        char c;
        int flag = 1;// РїРѕРєР° СЋР·РµСЂ РЅРµ РІРІРµР» /n
        while(flag){//РїРѕРєР° РЅРµ СЂР°РІРµРЅ 0
        scanf("%c", &c);
            if(c == '\n'){
                flag = 0;
            } else {// РµСЃР»Рё РЅРµ СЂР°РІРЅСЏРµС‚СЃСЏ С‚Рѕ Р·Р°РїРёСЃС‹РІР°РµРј
                if(c-'0' <= amount){
                    table[i][c-'0']++;
                }
            }
        }
    }

    printf("\n");
    int graph_check = 1;
    // РїСЂРѕРІРµСЂРєР° РєСЂРµСЃС‚РѕРј, РєР°Рє С‚РѕР»СЊРєРѕ РїРѕСЏРІР»СЏРµС‚СЃСЏ РєСЂРµСЃС‚ СЃРѕ РІСЃРµРјРё 0 РіСЂР°С„ СЃС‚Р°РЅРѕРІРёС‚СЃСЏ РЅРµСЃРІСЏР·Р°РЅРЅС‹Рј
    for(int i=0; i<amount; i++){
        int temp_graph_check = 0; 
        for(int j=0; j<amount; j++){
            if(table[i][j+1] == 1)
                temp_graph_check = 1;
    
            if(table[j][i+1] == 1)
                temp_graph_check = 1;
        }
        if(temp_graph_check == 0)
            graph_check=0;
    }
    
    if(graph_check == 0){
        printf("Р“СЂР°С„ РЅРµСЃРІСЏР·Р°РЅРЅС‹Р№\n");
    } else {
        printf("Р“СЂР°С„ СЃРІР·СЏР°РЅРЅС‹Р№\n");

    }
    printf("--------------------\n");

    for(int i=0; i<amount; i++) {
        
        printf("%c: ", table[i][0]);
        
        for (int j=1; j<amount+1; j++) {
            printf("%d  ", table[i][j]);
        }

        printf("\n");
    }

    char command[1024] = {0};
    char arrow[3] = "";
    
    strcat(command, "echo ' ");
    if(mode == 0){
        strcat(command, "digraph G {");
        strcat(arrow, "->");
    } else {
        strcat(command, "graph G {");
        strcat(arrow, "--");
    }
    
    Find(table, amount, arrow);

    for(int i=0; i<amount; i++){
        char elem[3] = "";
        elem[0] = table[i][0];
        strcat(command, elem);
        strcat(command, "; ");
    }
    for(int i=0; i<amount; i++){
        for(int j=0; j<amount; j++){
            for(int k=0; k<table[i][j+1]; k++){
                char elem[2] = "";
                elem[0] = table[i][0];
                
                strcat(command, elem);
                strcat(command, arrow);
                
                elem[0] = table[j][0];
                strcat(command, elem);
                strcat(command, "; ");
            }
        }
    }
    strcat(command, "}' | dot -Tpng > ./graph.png");
    system(command);
    
    return 0;
}
