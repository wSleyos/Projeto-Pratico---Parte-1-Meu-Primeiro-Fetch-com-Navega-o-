import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

// Criando o Stack
const Stack = createNativeStackNavigator();

// Tela Usuario
function TelaUsuario() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users/2')
      .then((response) => response.json())
      .then((data) => setUser(data))
      .catch((error) => console.error('Erro ao buscar usuário:', error));
  }, []);

  return (
    <View style={styles.container}>
      {user === null ? (
        <Text style={styles.carregando}>Carregando...</Text>
      ) : (
        <>
          <Text style={styles.titulo}>Usuário Encontrado 👤</Text>
          <Text style={styles.texto}>Nome: {user.name}</Text>
          <Text style={styles.texto}>Email: {user.email}</Text>
        </>
      )}
    </View>
  );
}

// App principal
export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="TelaUsuario"
          component={TelaUsuario}
          options={{ title: 'Dados do Usuário' }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

// Estilos
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f2f2f2',
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  carregando: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#555',
  },
  titulo: {
    fontSize: 26,
    fontWeight: 'bold',
    marginBottom: 20,
    textAlign: 'center',
  },
  texto: {
    fontSize: 20,
    marginBottom: 10,
    textAlign: 'center',
    color: '#333',
  },
});
