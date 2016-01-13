 # ClickandMoveUpdate.
 This script works only if you want the object to move by "click".


		 using UnityEngine;
			 using System.Collections;
		 		public class NomadClick : MonoBehaviour {
 
 
	 public int smooth; // Determines how quickly object moves towards position
	 	private Vector3 targetPosition;
   		public	int speed= 25;
			 Plane playerPlane; //public Plane groundPlane;
				 Ray ray; 
	 					public GameObject clickEffect;


	void Update (){
		if(Input.GetKeyDown(KeyCode.Mouse0)) {
			
			speed = 10;
				smooth=0;
		  	  Plane groundPlane= new Plane(Vector3.up, transform.position);
						Ray ray= Camera.main.ScreenPointToRay (Input.mousePosition);
								float rayDistance = 0.0f; //float  hitdist; // float rayDistance;

			 // The best overloaded method match for `UnityEngine.Plane.Raycast(UnityEngine.Ray, out float)' 
			//has some invalid arguments

			if (groundPlane.Raycast(ray, out rayDistance)) 
			{
				
			    targetPosition	= ray.GetPoint(rayDistance);
						targetPosition = ray.GetPoint(rayDistance);
							var targetRotation = Quaternion.LookRotation(targetPosition - transform.position);
							transform.rotation = targetRotation;

			}
		}

		Vector3 dir = targetPosition - transform.position;
			float dist = dir.magnitude;
			float move = speed * Time.deltaTime;
		
		if(dist > move){
			transform.position += dir.normalized * move;
				if (clickEffect != null)
				{
					Instantiate(clickEffect, targetPosition, Quaternion.identity);
				}
		
		}
		else {
			transform.position = targetPosition;
		}
		
			transform.position += (targetPosition - transform.position).normalized * speed * Time.deltaTime;

		}
	 }

 /*  After taking your script, it works. My problem is that when I use a KeyCode input to call another script like wanting the object to 
 follow me, it will try to follow me but cannot cause its seems like its stuck. I have a feeling that the collider of the 
 gameobject is interferring with terrain. I have provided my Follow script below. Here is the dillemma on how it happens.
 1. F1 press - displays menu  //Enables menu buttons
 2. 3 press - ClickAndMove script //.enabled = true & F1 options dissapear 
 3. F1 press - displays menu //Enables ClickAndMove
 4. 1 press - Follow the player// not wanting to follow player after the ClickAndMoveScript
 */

 //internet
				     using UnityEngine;
  					 using System.Collections;
 							public class Ship101 : MonoBehaviour {
							public Transform target; //FPS Shooter
							public int moveSpeed;
							public int rotationSpeed;
							public int maxdistance;
							private Transform myTransform;
	   

		void Awake()
			{
				myTransform = transform;
				myTransform.LookAt (target);

			}
	
	
		void Start ()
			{
		
				maxdistance = 10;
			}
	
	
		void Update ()
		{
			myTransform.LookAt (target);
		if (Vector3.Distance (target.position, myTransform.position) > maxdistance) {

			// Get a direction vector from us to the target
				Vector3 dir = target.position - myTransform.position;
			
			// Normalize it so that it's a unit direction vector
				dir.Normalize ();
			
					// Move ourselves in that direction
						myTransform.position += dir * moveSpeed * Time.deltaTime;

			}

				}

			 }


