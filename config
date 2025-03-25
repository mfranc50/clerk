import { ClerkProvider, SignedIn, SignedOut, SignIn, useAuth, useUser } from "@clerk/clerk-expo";
import { NavigationContainer } from "@react-navigation/native";
import { createStackNavigator } from "@react-navigation/stack";
import { View, Text, Button } from "react-native";

const CLERK_PUBLISHABLE_KEY = "clerk_publishable_key"; // Remplace par ta clé Clerk

const Stack = createStackNavigator();

export default function App() {
  return (
    <ClerkProvider publishableKey={CLERK_PUBLISHABLE_KEY}>
      <NavigationContainer>
        <Stack.Navigator screenOptions={{ headerShown: false }}>
          <Stack.Screen name="Auth" component={AuthScreen} />
          <Stack.Screen name="Dashboard" component={UserDashboard} />
        </Stack.Navigator>
      </NavigationContainer>
    </ClerkProvider>
  );
}

// 📌 Écran d'authentification (Connexion avec Clerk)
const AuthScreen = ({ navigation }) => {
  return (
    <>
      <SignedIn>
        {() => {
          navigation.replace("Dashboard"); // Redirige vers le tableau de bord après connexion
          return null;
        }}
      </SignedIn>

      <SignedOut>
        <SignIn
          appearance={{
            elements: {
              formButtonPrimary: {
                backgroundColor: "#007AFF",
                color: "white",
                borderRadius: 10,
              },
              card: {
                borderRadius: 15,
                borderWidth: 1,
                borderColor: "#ddd",
              },
            },
          }}
        />
      </SignedOut>
    </>
  );
};

// 📌 Écran du tableau de bord (Affiche infos + Déconnexion)
const UserDashboard = ({ navigation }) => {
  const { signOut } = useAuth();
  const { user } = useUser();

  return (
    <View style={{ flex: 1, justifyContent: "center", alignItems: "center", padding: 20 }}>
      <Text style={{ fontSize: 20, fontWeight: "bold", marginBottom: 10 }}>
        Bienvenue, {user.fullName} !
      </Text>
      <Text>Email : {user.primaryEmailAddress.emailAddress}</Text>
      <Button 
        title="Se déconnecter" 
        onPress={() => { 
          signOut(); 
          navigation.replace("Auth"); 
        }} 
      />
    </View>
  );
};
