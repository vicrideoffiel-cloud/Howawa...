# Howawa...
import React, { useState } from "react";
import {
  View,
  Text,
  StyleSheet,
  TouchableOpacity,
  SafeAreaView,
  StatusBar,
  useWindowDimensions
} from "react-native";

import Svg, {
  Defs,
  LinearGradient,
  RadialGradient,
  Stop,
  Rect,
  Circle,
  Ellipse,
  Path,
  G
} from "react-native-svg";

function EyeIcon({ color = "#ED1830" }) {
  return (
    <Svg width="42" height="32" viewBox="0 0 42 32">
      <Path
        d="M2 16 C10 2 32 2 40 16 C32 30 10 30 2 16Z"
        fill="white"
      />
      <Circle cx="21" cy="16" r="9" fill={color} />
      <Circle cx="21" cy="16" r="4" fill="white" />
    </Svg>
  );
}

function Illustration() {
  return (
    <Svg
      width="100%"
      height="100%"
      viewBox="0 0 360 520"
      preserveAspectRatio="xMidYMid meet"
    >
      <Defs>
        <LinearGradient id="pink" x1="0" y1="0" x2="1" y2="1">
          <Stop offset="0" stopColor="#FFFDFD" />
          <Stop offset="1" stopColor="#FCE8E9" />
        </LinearGradient>

        <RadialGradient id="shadow">
          <Stop offset="0" stopColor="#F4B9BC" stopOpacity="0.6" />
          <Stop offset="1" stopColor="#FFFFFF" stopOpacity="0" />
        </RadialGradient>

        <LinearGradient id="ball" x1="0" y1="0" x2="1" y2="1">
          <Stop offset="0" stopColor="#F28A53" />
          <Stop offset="1" stopColor="#A94121" />
        </LinearGradient>
      </Defs>

      {/* Background decoration */}
      <Ellipse
        cx="180"
        cy="230"
        rx="175"
        ry="190"
        fill="url(#shadow)"
      />

      <G rotation="-29" origin="180,240">
        <Rect
          x="5"
          y="75"
          width="350"
          height="340"
          rx="35"
          fill="url(#pink)"
        />

        {/* Central product frame */}
        <Rect
          x="82"
          y="145"
          width="200"
          height="135"
          rx="9"
          fill="#FFFFFF"
          stroke="#EF263D"
          strokeWidth="4"
        />

        <Ellipse
          cx="182"
          cy="220"
          rx="82"
          ry="45"
          fill="#D9D9D9"
          opacity="0.3"
        />

        {/* Basketball */}
        <Circle
          cx="182"
          cy="212"
          r="48"
          fill="url(#ball)"
        />

        <G
          stroke="#8D381F"
          strokeWidth="3"
          fill="none"
          opacity="0.85"
        >
          <Path d="M134 212 Q182 185 230 212" />
          <Path d="M134 212 Q182 239 230 212" />
          <Path d="M182 164 Q160 212 182 260" />
          <Path d="M182 164 Q204 212 182 260" />
        </G>
      </G>

      {/* Eye button left */}
      <Circle cx="75" cy="165" r="28" fill="white" />
      <Circle cx="75" cy="165" r="17" fill="#ED1830" />
      <EyeIcon />

      {/* Eye button right */}
      <Circle cx="305" cy="300" r="22" fill="#ED1830" />
      <G transform="translate(284 284)">
        <EyeIcon />
      </G>

      {/* Eye button bottom left */}
      <Rect
        x="54"
        y="330"
        width="90"
        height="64"
        rx="18"
        fill="#ED1830"
        rotation="-12"
        origin="99,362"
      />
      <G transform="translate(78 344)">
        <EyeIcon />
      </G>

      {/* White heart */}
      <Path
        d="M230 365 C215 345 190 357 205 379 C216 396 240 398 248 379 C257 359 239 347 230 365Z"
        fill="white"
      />

      {/* Decorative shape */}
      <Rect
        x="265"
        y="45"
        width="48"
        height="40"
        rx="12"
        fill="white"
        rotation="-25"
        origin="289,65"
      />
    </Svg>
  );
}

export default function App() {
  const [page, setPage] = useState(0);
  const { width, height } = useWindowDimensions();

  const pages = [
    {
      title: "Découvrez nos produits",
      description: "Explorez vos produits facilement."
    },
    {
      title: "Une expérience simple",
      description: "Profitez d'une navigation intuitive."
    },
    {
      title: "Tout est à votre portée",
      description: "Commencez votre expérience maintenant."
    }
  ];

  function nextPage() {
    if (page < 2) {
      setPage(page + 1);
    } else {
      setPage(0);
    }
  }

  return (
    <SafeAreaView style={styles.safe}>
      <StatusBar
        backgroundColor="#FFFFFF"
        barStyle="dark-content"
      />

      <View style={styles.container}>

        {/* Illustration */}
        <View
          style={[
            styles.illustration,
            { height: height * 0.66 }
          ]}
        >
          <Illustration />
        </View>

        {/* Textes */}
        <View style={styles.textArea}>
          <Text style={styles.title}>
            {pages[page].title}
          </Text>

          <Text style={styles.description}>
            {pages[page].description}
          </Text>
        </View>

        {/* Bottom navigation */}
        <View style={styles.bottom}>

          <View style={styles.dots}>
            {[0, 1, 2].map((item) => (
              <View
                key={item}
                style={[
                  styles.dot,
                  page === item && styles.activeDot
                ]}
              />
            ))}
          </View>

          <TouchableOpacity
            style={styles.nextButton}
            onPress={nextPage}
            activeOpacity={0.8}
          >
            <Text style={styles.nextText}>
              {page === 2 ? "Commencer" : "Suivant"}
            </Text>
          </TouchableOpacity>

        </View>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safe: {
    flex: 1,
    backgroundColor: "#FFFFFF"
  },

  container: {
    flex: 1,
    backgroundColor: "#FFFFFF"
  },

  illustration: {
    width: "100%",
    justifyContent: "center",
    alignItems: "center"
  },

  textArea: {
    alignItems: "center",
    paddingHorizontal: 25,
    flex: 1,
    justifyContent: "center"
  },

  title: {
    color: "#222222",
    fontSize: 22,
    fontWeight: "bold",
    textAlign: "center"
  },

  description: {
    color: "#888888",
    fontSize: 14,
    marginTop: 10,
    textAlign: "center"
  },

  bottom: {
    height: 100,
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between",
    paddingHorizontal: 28,
    paddingBottom: 10
  },

  dots: {
    flexDirection: "row",
    alignItems: "center",
    gap: 12
  },

  dot: {
    width: 12,
    height: 12,
    borderRadius: 10,
    backgroundColor: "#D9D9D9"
  },

  activeDot: {
    backgroundColor: "#ED2637"
  },

  nextButton: {
    width: 165,
    height: 58,
    borderRadius: 35,
    backgroundColor: "#ED2637",
    justifyContent: "center",
    alignItems: "center"
  },

  nextText: {
    color: "#FFFFFF",
    fontSize: 19,
    fontWeight: "500"
  }
});

{
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    }
  }
}
npm install -g eas-cli
eas login
eas build:configure
eas build -p android --profile preview<G transform="translate(54 149)">
  <EyeIcon />
import React, { useState } from "react";
import {
  View,
  Text,
  Image,
  StyleSheet,
  SafeAreaView,
  TouchableOpacity,
  StatusBar,
  useWindowDimensions
} from "react-native";

import Svg, { Path, Circle, Rect } from "react-native-svg";

const RED = "#F0203D";

function Icon({ type, color = RED, size = 48 }) {
  const paths = {
    eye: (
      <>
        <Path
          d="M3 24 Q24 -2 45 24 Q24 50 3 24Z"
          stroke={color}
          strokeWidth="3"
          fill="none"
        />
        <Circle cx="24" cy="24" r="9" stroke={color}
          strokeWidth="3" fill="none" />
      </>
    ),
    hanger: (
      <>
        <Path
          d="M24 8 C24 1 34 2 34 9 C34 13 29 14 27 18"
          stroke={color} strokeWidth="3" fill="none"
        />
        <Path
          d="M24 18 L4 34 Q2 37 7 37 H41 Q46 37 44 34 L24 18Z"
          stroke={color} strokeWidth="3"
          strokeLinejoin="round" fill="none"
        />
      </>
    ),
    play: (
      <Path
        d="M15 7 L40 24 L15 41 Q10 44 10 38 V10 Q10 4 15 7Z"
        stroke={color} strokeWidth="3"
        fill="none"
      />
    ),
    crown: (
      <Path
        d="M5 14 L15 23 L24 7 L33 23 L43 14 L38 39 H10Z"
        stroke={color} strokeWidth="3"
        strokeLinejoin="round" fill="none"
      />
    )
  };

  return (
    <Svg width={size} height={size} viewBox="0 0 48 48">
      {paths[type]}
    </Svg>
  );
}

function ProductCard({
  image,
  style,
  imageStyle,
  lines = true
}) {
  return (
    <View style={[styles.productCard, style]}>
      <Image
        source={{ uri: image }}
        style={[styles.productImage, imageStyle]}
        resizeMode="contain"
      />

      {lines && (
        <View style={styles.descriptionLines}>
          <View style={styles.longLine} />
          <View style={styles.shortLine} />
        </View>
      )}
    </View>
  );
}

export default function App() {
  const [page, setPage] = useState(1);
  const { width, height } = useWindowDimensions();

  const images = {
    shoe: "https://images.unsplash.com/photo-1552346154-21d32810aba3?w=700",
    hoodie: "https://images.unsplash.com/photo-1556821840-3a63f95609a7?w=700",
    pants: "https://images.unsplash.com/photo-1552902865-b72c031ac5ea?w=700",
    tshirt: "https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=700"
  };

  return (
    <SafeAreaView style={styles.safe}>
      <StatusBar
        backgroundColor="#FFFFFF"
        barStyle="dark-content"
      />

      <View style={styles.container}>

        {/* Décor rose */}
        <View style={styles.pinkGlow} />
        <View style={styles.pinkGlowTwo} />

        {/* Carte sweat */}
        <ProductCard
          image={images.hoodie}
          style={[
            styles.hoodieCard,
            { width: width * 0.48, height: height * 0.24 }
          ]}
        />

        {/* Carte pantalon */}
        <ProductCard
          image={images.pants}
          style={[
            styles.pantsCard,
            { width: width * 0.42, height: height * 0.24 }
          ]}
        />

        {/* Carte centrale */}
        <View
          style={[
            styles.mainCard,
            {
              width: width * 0.68,
              height: height * 0.29
            }
          ]}
        >
          <View style={styles.shoeFrame}>
            <Image
              source={{ uri: images.shoe }}
              style={styles.shoeImage}
              resizeMode="contain"
            />
          </View>

          <View style={styles.mainDescription}>
            <View style={styles.avatar} />
            <View style={styles.lines}>
              <View style={styles.longLine} />
              <View style={styles.shortLine} />
            </View>
          </View>
        </View>

        {/* Carte T-shirt */}
        <ProductCard
          image={images.tshirt}
          style={[
            styles.tshirtCard,
            { width: width * 0.43, height: height * 0.23 }
          ]}
        />

        {/* Icône œil */}
        <View style={styles.eyeButton}>
          <Icon type="eye" color="white" size={65} />
        </View>

        {/* Icône cintre */}
        <View style={styles.hangerButton}>
          <Icon type="hanger" size={52} />
        </View>

        {/* Icône lecture */}
        <View style={styles.playButton}>
          <Icon type="play" color="white" size={50} />
        </View>

        {/* Icône couronne */}
        <View style={styles.crownButton}>
          <Icon type="crown" color="white" size={62} />
        </View>

        {/* Cœur */}
        <Text style={styles.heart}>♥</Text>

        {/* Progression et bouton */}
        <View style={styles.bottom}>
          <View style={styles.dots}>
            {[0, 1, 2].map((item) => (
              <View
                key={item}
                style={[
                  styles.dot,
                  page === item && styles.activeDot
                ]}
              />
            ))}
          </View>

          <TouchableOpacity
            style={styles.nextButton}
            onPress={() => setPage(page === 2 ? 0 : page + 1)}
            activeOpacity={0.8}
          >
            <Text style={styles.nextText}>
              {page === 2 ? "Commencer" : "Suivant"}
            </Text>
          </TouchableOpacity>
        </View>

      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safe: {
    flex: 1,
    backgroundColor: "#FFFFFF"
  },

  container: {
    flex: 1,
    backgroundColor: "#FFFFFF",
    overflow: "hidden"
  },

  pinkGlow: {
    position: "absolute",
    width: 280,
    height: 280,
    borderRadius: 150,
    backgroundColor: "#FFF0F1",
    top: 70,
    left: 80
  },

  pinkGlowTwo: {
    position: "absolute",
    width: 250,
    height: 300,
    borderRadius: 150,
    backgroundColor: "#FFF1F2",
    top: 400,
    right: -100
  },

  productCard: {
    position: "absolute",
    backgroundColor: "#FFFAFA",
    borderRadius: 20,
    padding: 12,
    elevation: 3,
    shadowColor: "#F3AAB2",
    shadowOpacity: 0.18,
    shadowRadius: 15
  },

  hoodieCard: {
    top: "13%",
    left: "13%",
    transform: [{ rotate: "-19deg" }],
    zIndex: 1
  },

  pantsCard: {
    top: "19%",
    right: "4%",
    transform: [{ rotate: "-19deg" }],
    zIndex: 1
  },

  tshirtCard: {
    top: "55%",
    right: "-1%",
    transform: [{ rotate: "-19deg" }],
    zIndex: 1
  },

  productImage: {
    width: "100%",
    height: "82%"
  },

  descriptionLines: {
    marginTop: 5,
    alignItems: "center"
  },

  longLine: {
    width: "75%",
    height: 9,
    borderRadius: 10,
    backgroundColor: "#E8E1E3"
  },

  shortLine: {
    width: "55%",
    height: 8,
    borderRadius: 10,
    backgroundColor: "#E8E1E3",
    marginTop: 6
  },

  mainCard: {
    position: "absolute",
    top: "29%",
    left: "15%",
    backgroundColor: "#FFFFFF",
    borderRadius: 22,
    padding: 13,
    transform: [{ rotate: "-19deg" }],
    zIndex: 5,
    elevation: 12,
    shadowColor: "#E83C50",
    shadowOpacity: 0.23,
    shadowRadius: 20
  },

  shoeFrame: {
    flex: 1,
    borderWidth: 5,
    borderColor: RED,
    borderRadius: 10,
    overflow: "hidden",
    backgroundColor: "#FFF0F1"
  },

  shoeImage: {
    width: "100%",
    height: "100%"
  },

  mainDescription: {
    height: "20%",
    flexDirection: "row",
    alignItems: "center",
    paddingHorizontal: 8
  },

  avatar: {
    width: 34,
    height: 34,
    borderRadius: 20,
    backgroundColor: "#F0DADD",
    marginRight: 10
  },

  lines: {
    flex: 1,
    gap: 6
  },

  eyeButton: {
    position: "absolute",
    top: "27%",
    left: "8%",
    width: 115,
    height: 110,
    borderRadius: 60,
    backgroundColor: RED,
    alignItems: "center",
    justifyContent: "center",
    zIndex: 7
  },

  hangerButton: {
    position: "absolute",
    top: "14%",
    right: "9%",
    width: 105,
    height: 100,
    borderRadius: 60,
    backgroundColor: "white",
    alignItems: "center",
    justifyContent: "center",
    zIndex: 7
  },

  playButton: {
    position: "absolute",
    top: "42%",
    right: "8%",
    width: 105,
    height: 105,
    borderRadius: 60,
    backgroundColor: RED,
    alignItems: "center",
    justifyContent: "center",
    zIndex: 7
  },

  crownButton: {
    position: "absolute",
    top: "52%",
    left: "12%",
    width: 155,
    height: 125,
    borderRadius: 25,
    backgroundColor: RED,
    alignItems: "center",
    justifyContent: "center",
    transform: [{ rotate: "-18deg" }],
    zIndex: 7
  },

  heart: {
    position: "absolute",
    top: "63%",
    left: "48%",
    color: "white",
    fontSize: 85,
    zIndex: 8
  },

  bottom: {
    position: "absolute",
    bottom: 20,
    left: 0,
    right: 0,
    height: 90,
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between",
    paddingHorizontal: 35,
    zIndex: 10
  },

  dots: {
    flexDirection: "row",
    gap: 13,
    alignItems: "center"
  },

  dot: {
    width: 14,
    height: 14,
    borderRadius: 10,
    backgroundColor: "#D5D5D5"
  },

  activeDot: {
    backgroundColor: RED
  },

  nextButton: {
    width: 185,
    height: 75,
    backgroundColor: RED,
    borderRadius: 45,
    alignItems: "center",
    justifyContent: "center"
  },

  nextText: {
    fontSize: 27,
    color: "#FFFFFF",
    fontWeight: "500"
  }
});
npx create-expo-app@latest MonApplication
cd MonApplication

npx expo install react-native-svg

npm install -g eas-cli

eas login
eas build:configure
</G>npx expo install react-native-svg{
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    }
  }
}eas build -p android --profile pr
eview
import React, { useState } from "react";

import {
  View,
  Text,
  Image,
  StyleSheet,
  SafeAreaView,
  StatusBar,
  TouchableOpacity,
  Alert,
  useWindowDimensions
} from "react-native";

import Svg, { Path, Circle } from "react-native-svg";

const RED = "#F21D35";

const products = [
  {
    name: "Sweat à capuche",
    image: "https://images.unsplash.com/photo-1556821840-3a63f95609a7?w=500",
    position: "topLeft"
  },
  {
    name: "Pantalon de sport",
    image: "https://images.unsplash.com/photo-1552902865-b72c031ac5ea?w=500",
    position: "topRight"
  },
  {
    name: "T-shirt",
    image: "https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=500",
    position: "bottomLeft"
  },
  {
    name: "Ensemble complet",
    image: "https://images.unsplash.com/photo-1506629905607-d9e9f5d4c9f0?w=500",
    position: "bottomRight"
  }
];

function HeartIcon() {
  return (
    <Svg width={23} height={23} viewBox="0 0 24 24">
      <Path
        d="M12 21S2 14.5 2 8.5C2 3 9 2 12 7C15 2 22 3 22 8.5C22 14.5 12 21 12 21Z"
        fill="#D5D0D2"
      />
    </Svg>
  );
}

function PlayIcon() {
  return (
    <Svg width={23} height={23} viewBox="0 0 24 24">
      <Path
        d="M7 4L20 12L7 20Z"
        fill="white"
      />
    </Svg>
  );
}

function ProductCard({ image, position, width, height }) {
  const positionStyles = {
    topLeft: {
      top: "16%",
      left: "7%"
    },
    topRight: {
      top: "19%",
      right: "5%"
    },
    bottomLeft: {
      top: "39%",
      left: "7%"
    },
    bottomRight: {
      top: "43%",
      right: "4%"
    }
  };

  return (
    <View
      style={[
        styles.card,
        {
          width,
          height,
          ...positionStyles[position],
          transform: [{ rotate: "-17deg" }]
        }
      ]}
    >
      {/* Product photo */}
      <Image
        source={{ uri: image }}
        style={styles.productImage}
        resizeMode="contain"
      />

      {/* Favorite */}
      <View style={styles.heartButton}>
        <HeartIcon />
      </View>

      {/* Play */}
      <View style={styles.playButton}>
        <PlayIcon />
      </View>

      {/* Description */}
      <View style={styles.description}>
        <View style={styles.avatar} />

        <View style={styles.textLines}>
          <View style={styles.lineOne} />
          <View style={styles.lineTwo} />
        </View>
      </View>
    </View>
  );
}

export default function App() {
  const { width, height } = useWindowDimensions();

  const [started, setStarted] = useState(false);

  const cardWidth = width * 0.46;
  const cardHeight = height * 0.215;

  const startApp = () => {
    setStarted(true);
  };

  if (started) {
    return (
      <SafeAreaView style={styles.safe}>
        <View style={styles.welcome}>
          <Text style={styles.welcomeTitle}>
            Bienvenue !
          </Text>

          <Text style={styles.welcomeText}>
            Votre expérience commence maintenant.
          </Text>

          <TouchableOpacity
            style={styles.nextButton}
            onPress={() => setStarted(false)}
          >
            <Text style={styles.nextText}>
              Retour
            </Text>
          </TouchableOpacity>
        </View>
      </SafeAreaView>
    );
  }

  return (
    <SafeAreaView style={styles.safe}>
      <StatusBar
        backgroundColor="#FFFFFF"
        barStyle="dark-content"
      />

      <View style={styles.container}>

        {/* Background glow */}
        <View style={styles.glowOne} />
        <View style={styles.glowTwo} />
        <View style={styles.glowThree} />

        {/* Four product cards */}
        {products.map((product, index) => (
          <ProductCard
            key={index}
            image={product.image}
            position={product.position}
            width={cardWidth}
            height={cardHeight}
          />
        ))}

        {/* Decorative pink circle */}
        <View style={styles.decorativeCircle} />

        {/* Bottom navigation */}
        <View style={styles.bottom}>

          <View style={styles.progress}>
            {[0, 1, 2].map((item) => (
              <View
                key={item}
                style={[
                  styles.dot,
                  item === 2 && styles.activeDot
                ]}
              />
            ))}
          </View>

          <TouchableOpacity
            style={styles.startButton}
            onPress={startApp}
            activeOpacity={0.8}
          >
            <Text style={styles.startText}>
              Démarrer
            </Text>
          </TouchableOpacity>

        </View>

      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({

  safe: {
    flex: 1,
    backgroundColor: "#FFFFFF"
  },

  container: {
    flex: 1,
    backgroundColor: "#FFFFFF",
    overflow: "hidden"
  },

  glowOne: {
    position: "absolute",
    top: "12%",
    left: "25%",
    width: 250,
    height: 250,
    borderRadius: 150,
    backgroundColor: "#FFF0F1"
  },

  glowTwo: {
    position: "absolute",
    top: "30%",
    left: "-15%",
    width: 300,
    height: 300,
    borderRadius: 150,
    backgroundColor: "#FCE7E9",
    opacity: 0.6
  },

  glowThree: {
    position: "absolute",
    top: "40%",
    right: "-20%",
    width: 250,
    height: 250,
    borderRadius: 150,
    backgroundColor: "#FFF0F1"
  },

  card: {
    position: "absolute",
    backgroundColor: "#FFFEFE",
    borderRadius: 20,
    padding: 10,
    elevation: 5,
    shadowColor: "#ECAAB1",
    shadowOpacity: 0.18,
    shadowRadius: 15,
    zIndex: 3
  },

  productImage: {
    width: "100%",
    height: "72%",
    borderRadius: 12
  },

  heartButton: {
    position: "absolute",
    top: 8,
    right: 8,
    width: 34,
    height: 34,
    borderRadius: 20,
    backgroundColor: "#FFFFFF",
    alignItems: "center",
    justifyContent: "center",
    elevation: 2
  },

  playButton: {
    position: "absolute",
    left: 12,
    bottom: "19%",
    width: 43,
    height: 43,
    borderRadius: 25,
    backgroundColor: RED,
    alignItems: "center",
    justifyContent: "center"
  },

  description: {
    flexDirection: "row",
    alignItems: "center",
    flex: 1,
    paddingHorizontal: 5,
    marginTop: 5
  },

  avatar: {
    width: 30,
    height: 30,
    borderRadius: 20,
    backgroundColor: "#E8E4E5",
    marginRight: 8
  },

  textLines: {
    flex: 1,
    gap: 6
  },

  lineOne: {
    height: 7,
    width: "90%",
    borderRadius: 10,
    backgroundColor: "#E7E1E3"
  },

  lineTwo: {
    height: 7,
    width: "65%",
    borderRadius: 10,
    backgroundColor: "#E7E1E3"
  },

  decorativeCircle: {
    position: "absolute",
    top: "23%",
    right: "5%",
    width: 26,
    height: 26,
    borderRadius: 20,
    backgroundColor: "#F78B99",
    elevation: 5
  },

  bottom: {
    position: "absolute",
    bottom: 55,
    left: 0,
    right: 0,
    height: 90,
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between",
    paddingHorizontal: 35,
    zIndex: 10
  },

  progress: {
    flexDirection: "row",
    alignItems: "center",
    gap: 12
  },

  dot: {
    width: 13,
    height: 13,
    borderRadius: 10,
    backgroundColor: "#D7D7D7"
  },

  activeDot: {
    backgroundColor: RED
  },

  startButton: {
    width: 185,
    height: 65,
    borderRadius: 40,
    backgroundColor: RED,
    alignItems: "center",
    justifyContent: "center"
  },

  startText: {
    color: "#FFFFFF",
    fontSize: 25,
    fontWeight: "500"
  },

  welcome: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 25
  },

  welcomeTitle: {
    fontSize: 32,
    fontWeight: "bold",
    color: RED
  },

  welcomeText: {
    fontSize: 16,
    color: "#777777",
    marginTop: 15,
    textAlign: "center"
  },

  nextButton: {
    marginTop: 30,
    backgroundColor: RED,
    paddingHorizontal: 40,
    paddingVertical: 15,
    borderRadius: 30
  },

  nextText: {
    color: "white",
    fontSize: 18
  }

});
npx create-expo-app@latest MonApplication
cd MonApplication

npx expo install react-native-svg

npm install -g eas-cli

eas login
eas build:configure{
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    }
  }
}eas build -p android --profile preview
import React, { useState } from "react";
import {
  View,
  Text,
  StyleSheet,
  SafeAreaView,
  TouchableOpacity,
  StatusBar,
  useWindowDimensions
} from "react-native";

import Svg, {
  Rect,
  Circle,
  Ellipse,
  Path,
  G,
  Defs,
  LinearGradient,
  RadialGradient,
  Stop
} from "react-native-svg";

const RED = "#EF1833";

// Icône œil
function Eye({ size = 48 }) {
  return (
    <Svg width={size} height={size * 0.75}
      viewBox="0 0 48 36">
      <Path
        d="M2 18 Q24 -7 46 18 Q24 43 2 18Z"
        fill="white"
      />
      <Circle cx="24" cy="18" r="11" fill={RED} />
      <Circle cx="24" cy="18" r="5" fill="white" />
    </Svg>
  );
}

// Illustration centrale
function BasketballIllustration() {
  return (
    <Svg
      width="100%"
      height="100%"
      viewBox="0 0 360 440"
    >
      <Defs>
        <LinearGradient
          id="background"
          x1="0" y1="0" x2="1" y2="1"
        >
          <Stop offset="0" stopColor="#FFFFFF" />
          <Stop offset="1" stopColor="#FCE8E9" />
        </LinearGradient>

        <RadialGradient id="pinkGlow">
          <Stop offset="0" stopColor="#F7C4C9" stopOpacity="0.7" />
          <Stop offset="1" stopColor="#FFFFFF" stopOpacity="0" />
        </RadialGradient>

        <LinearGradient id="basketball" x1="0" y1="0" x2="1" y2="1">
          <Stop offset="0" stopColor="#F18B55" />
          <Stop offset="1" stopColor="#A84221" />
        </LinearGradient>
      </Defs>

      {/* Lumière rose */}
      <Ellipse
        cx="180"
        cy="210"
        rx="180"
        ry="210"
        fill="url(#pinkGlow)"
      />

      {/* Grande carte inclinée */}
      <G rotation="-32" origin="180,205">
        <Rect
          x="-5"
          y="50"
          width="370"
          height="330"
          rx="35"
          fill="url(#background)"
        />

        {/* Petit carré décoratif */}
        <Rect
          x="280"
          y="65"
          width="55"
          height="45"
          rx="13"
          fill="white"
        />

        {/* Cadre rouge central */}
        <Rect
          x="77"
          y="145"
          width="220"
          height="140"
          rx="8"
          fill="#FFFDFD"
          stroke={RED}
          strokeWidth="5"
        />

        {/* Ombre du ballon */}
        <Ellipse
          cx="187"
          cy="250"
          rx="72"
          ry="17"
          fill="#9D7770"
          opacity="0.17"
        />

        {/* Ballon de basket */}
        <Circle
          cx="187"
          cy="210"
          r="54"
          fill="url(#basketball)"
        />

        {/* Coutures du ballon */}
        <G
          stroke="#8D3C25"
          strokeWidth="3"
          fill="none"
          opacity="0.9"
        >
          <Path d="M133 210 Q187 178 241 210" />
          <Path d="M133 210 Q187 243 241 210" />
          <Path d="M187 156 Q160 210 187 264" />
          <Path d="M187 156 Q214 210 187 264" />
        </G>

        {/* Détails du ballon */}
        <Circle cx="187" cy="164" r="4" fill="#8D3C25" />
        <Path
          d="M160 202 Q187 194 216 202"
          stroke="#77351F"
          strokeWidth="2"
          fill="none"
        />
      </G>
    </Svg>
  );
}

// Bouton œil
function EyeButton({ style, size = 48 }) {
  return (
    <View style={[styles.eyeButton, style]}>
      <Eye size={size} />
    </View>
  );
}

export default function App() {
  const [page, setPage] = useState(0);
  const { width, height } = useWindowDimensions();

  const nextPage = () => {
    setPage((old) => (old + 1) % 3);
  };

  return (
    <SafeAreaView style={styles.safe}>
      <StatusBar
        backgroundColor="#FFFFFF"
        barStyle="dark-content"
      />

      <View style={styles.container}>

        {/* Effets lumineux */}
        <View style={styles.glowOne} />
        <View style={styles.glowTwo} />

        {/* Illustration */}
        <View
          style={[
            styles.illustration,
            { height: height * 0.64 }
          ]}
        >
          <BasketballIllustration />
        </View>

        {/* Œil en haut à gauche */}
        <EyeButton
          style={{
            top: height * 0.20,
            left: width * 0.13,
            backgroundColor: "white",
            width: 110,
            height: 90
          }}
          size={55}
        />

        {/* Œil à droite */}
        <EyeButton
          style={{
            top: height * 0.35,
            right: width * 0.08,
            backgroundColor: RED,
            width: 88,
            height: 75
          }}
          size={45}
        />

        {/* Œil en bas à gauche */}
        <EyeButton
          style={{
            top: height * 0.41,
            left: width * 0.19,
            backgroundColor: RED,
            width: 135,
            height: 105,
            borderRadius: 25,
            transform: [{ rotate: "-15deg" }]
          }}
          size={55}
        />

        {/* Petit cœur blanc */}
        <Text
          style={[
            styles.heart,
            {
              top: height * 0.47,
              left: width * 0.58
            }
          ]}
        >
          ♥
        </Text>

        {/* Navigation en bas */}
        <View style={styles.bottom}>

          <View style={styles.dots}>
            {[0, 1, 2].map((item) => (
              <View
                key={item}
                style={[
                  styles.dot,
                  page === item && styles.activeDot
                ]}
              />
            ))}
          </View>

          <TouchableOpacity
            style={styles.nextButton}
            onPress={nextPage}
            activeOpacity={0.8}
          >
            <Text style={styles.nextText}>
              Suivant
            </Text>
          </TouchableOpacity>

        </View>

      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safe: {
    flex: 1,
    backgroundColor: "#FFFFFF"
  },

  container: {
    flex: 1,
    backgroundColor: "#FFFFFF",
    overflow: "hidden"
  },

  glowOne: {
    position: "absolute",
    width: 300,
    height: 300,
    borderRadius: 200,
    backgroundColor: "#FFF1F2",
    top: 80,
    left: 30
  },

  glowTwo: {
    position: "absolute",
    width: 260,
    height: 260,
    borderRadius: 200,
    backgroundColor: "#FCE9EA",
    top: 350,
    right: -100,
    opacity: 0.6
  },

  illustration: {
    width: "100%",
    justifyContent: "center",
    alignItems: "center"
  },

  eyeButton: {
    position: "absolute",
    justifyContent: "center",
    alignItems: "center",
    borderRadius: 60,
    elevation: 5,
    shadowColor: "#ED5366",
    shadowOpacity: 0.15,
    shadowRadius: 15,
    zIndex: 5
  },

  heart: {
    position: "absolute",
    color: "white",
    fontSize: 65,
    zIndex: 5
  },

  bottom: {
    position: "absolute",
    bottom: 55,
    left: 0,
    right: 0,
    height: 85,
    paddingHorizontal: 35,
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between"
  },

  dots: {
    flexDirection: "row",
    alignItems: "center",
    gap: 12
  },

  dot: {
    width: 13,
    height: 13,
    borderRadius: 10,
    backgroundColor: "#D5D5D5"
  },

  activeDot: {
    backgroundColor: RED
  },

  nextButton: {
    width: 185,
    height: 65,
    borderRadius: 40,
    backgroundColor: RED,
    justifyContent: "center",
    alignItems: "center",
    elevation: 3
  },

  nextText: {
    fontSize: 25,
    color: "#FFFFFF",
    fontWeight: "500"
  }
});npx create-expo-app@latest MonApplication
cd MonApplication
npx expo install react-native-svgnpm install -g eas-cli
eas login
eas build:configure
eas build -p android --profile preview
