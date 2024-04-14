import cv2
import numpy as np

# Définition des paramètres de la vidéo
fps = 24
video_length = 10  # en secondes
frame_width = 640
frame_height = 480

# Création d'un objet VideoWriter
out = cv2.VideoWriter('generated_video.avi', cv2.VideoWriter_fourcc(*'XVID'), fps, (frame_width, frame_height))

# Boucle pour générer chaque frame de la vidéo
for frame_number in range(video_length * fps):
    # Création d'une image aléatoire pour chaque frame
    frame = np.random.randint(0, 255, (frame_height, frame_width, 3), dtype=np.uint8)
    
    # Ajout du texte avec le numéro de la frame
    cv2.putText(frame, f'Frame: {frame_number}', (50, 50), cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)
    
    # Écriture de la frame dans la vidéo
    out.write(frame)
    
    # Affichage de la frame générée
    cv2.imshow('Generated Video', frame)
    
    # Attendre 1/fps seconde avant de passer à la frame suivante
    cv2.waitKey(1000 // fps)

# Libération des ressources
out.release()
cv2.destroyAllWindows()
