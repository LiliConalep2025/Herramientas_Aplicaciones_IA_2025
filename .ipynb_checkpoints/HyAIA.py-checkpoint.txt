#Clase que representa todo lo que veremos
class HyAIA:
    def __init__(self, df): #Método cosntructor
        self.data = df #Atributos (Df original)
        self.columns = df.columns #Columnas originales
        self.data_binarios, self.binarios_columns = self.get_binarios() #Atributos para binarios
        self.data_cuantitativos, self.cuantitativos_columns = self.get_cuantitativos() #Atributos para cuantitativos
        self.data_categoricos, self.categoricos_columns = self.get_categoricos() #Atributos categoricos
        
    ##% Métodos para Análisis de Datos 
    #Método para obtener las columnas y dataframe binarios
    def get_binarios(self):
        col_bin = [] #Lista vacía
        for col in self.data.columns:
            if self.data[col].nunique() == 2: #Numeros de elementos de valor único (" binaria)
                col_bin.append(col)
        return self.data[col_bin],col_bin #Retornar una tupla

    
    #Método para obtener columnas y dataframe cuantitativos
    def get_cuantitativos(self):
        col_cuantitativas = self.data.select_dtypes(include='number').columns #Selecciono los tipos de datos que tienen numeros    
        return self.data[col_cuantitativas], col_cuantitativas
        
       
    #Método para obtener columnas y dataframe categóricos
    def get_categoricos(self):
        col_categoricos = self.data.select_dtypes(exclude ='number').columns #Exluye los numeros y devuelve columnas
        col_cat = [] #Lista vacía
        for col in col_categoricos:
            if self.data[col].nunique()>2: #No valores numericos =< a 2
                col_cat.append(col) #Columnas categoricas s/binarias
        return self.data[col_cat], col_cat