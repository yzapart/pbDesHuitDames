public class huitDames {

	public static void main(String[] args) {

		String impasses[] = new String[1000000];
		int nbImpasses = 0;

		String solutions[] = new String[1000];
		int nbSolutions = 0;

		// boucle des chemins
		int N_CHEMINS = 13000;
		for (int chemin = 0; chemin < N_CHEMINS; chemin++) {
			// nouvel échiquier et chemin vierge
			int m[][] = initM();
			String cheminActuel = "";

			for (int colDep = 0; colDep < 8; colDep++) {
				for (int ligne = 0; ligne < 8; ligne++) {
					if (lignePleine(ligne, m) == true) {
						// la ligne est pleine, le chemin actuel devient une impasse
						impasses[nbImpasses] = cheminActuel;
						nbImpasses += 1;
						// il faut abandonner et recommencer un tout nouveau chemin sur un échiquier
						break;
					} else {
						// il y a possibilité de placer une dame, on boucle les cases et teste si elles
						// sont libres.
						for (int colonne = colDep; colonne < (colDep + 8); colonne++) {
							if (caseLibre(m, ligne, colonne % 8) == true) {
								// maintenant on vérifie si le chemin éventuel se situe dans la liste des
								// impasses
								if (estCheminInterdit((cheminActuel + String.valueOf(colonne % 8)), impasses) == true) {
									// le chemin éventuel est une impasse, on saute l'itération loop ('continue' à
									// la colonne suivante
									continue;
								} else {
									// le chemin éventuel n'est pas listé dans les impasses
									placerDame(m, ligne, colonne % 8);
									cheminActuel += String.valueOf(colonne % 8);
									if (cheminActuel.length() == 8) {
										solutions[nbSolutions] = cheminActuel;
										nbSolutions += 1;
										System.out.println("solution n°" + nbSolutions + " : " + cheminActuel
												+ "    chemin n° " + chemin);
										afficherEchiquier(m);
									}
								}
							}
						}
					}
				}
			}
		}
		System.out.println("--- " + nbSolutions + " solutions :  ---");
		for (int x = 0; x < nbSolutions; x++) {
			System.out.println(solutions[x]);
		}
	}

	// ----------------------------------------------- méthodes
	// ----------------------------------------------- //

	public static void afficherChemin(String chemin) {
		int m[][] = initM();
		for (int i = 0; i < chemin.length(); i++) {
			placerDame(m, i, Integer.valueOf(chemin.charAt(i)));
		}
		afficherEchiquier(m);
	}

	public static void afficherImpasses(String impasses[], int nb) {
		System.out.println("--- impasses (" + nb + ") : ---");
		for (int i = 0; i < nb; i++) {
			System.out.println(impasses[i]);
		}
	}

	public static boolean estCheminInterdit(String chemin, String cheminsInterdits[]) {
		for (int i = 0; i < cheminsInterdits.length; i++) {
			if (chemin.equals(cheminsInterdits[i]) == true) {
				return true;
			}
		}
		return false;
	}

	public static int[][] initM() {
		int m[][] = { { 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0 },
				{ 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0 },
				{ 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0 } };
		return m;
	}

	public static boolean lignePleine(int ligne, int m[][]) {
		boolean res = true;
		for (int i = 0; i < 8; i++) {
			if (m[ligne][i] == 0) {
				res = false;
			}
		}
		return res;
	}

	public static void afficherEchiquier(int m[][]) {
		for (int i = 0; i < m.length; i++) {
			for (int j = 0; j < m[i].length; j++) {
				System.out.print(m[i][j] + " ");
			}
			System.out.println();
		}
		System.out.println("---------------");
	}

	public static boolean caseLibre(int m[][], int ligne, int colonne) {
		boolean res = (m[ligne][colonne] == 1 || m[ligne][colonne] == 6) ? false : true;
		return res;
	}

	// placer une dame sur l'échiquier
	public static void placerDame(int m[][], int ligne, int colonne) {
		if (caseLibre(m, ligne, colonne) == true) {
			// case occupée : 6
			m[ligne][colonne] = 6;

			// cases menacée : 1
			for (int k = 1; k < 8; k++) {

				// ligne menacée
				m[ligne][(colonne + k) % 8] = 1;

				// colonne menacée
				m[(ligne + k) % 8][colonne] = 1;

				// diagonales menacées
				if ((ligne + k) < 8 && (colonne + k) < 8) {
					m[ligne + k][colonne + k] = 1;
				}
				if ((ligne + k) < 8 && (colonne - k) >= 0) {
					m[ligne + k][colonne - k] = 1;
				}
				if ((ligne - k) >= 0 && (colonne + k) < 8) {
					m[ligne - k][colonne + k] = 1;
				}
				if ((ligne - k) >= 0 && (colonne - k) >= 0) {
					m[ligne - k][colonne - k] = 1;
				}
			}
		} else {
			System.out.println("La case (" + ligne + ", " + colonne + ") n'est pas libre");
		}
	}

}
