# 2D-Portals-concept
A 2D representation of the concept used to design portals (Inspired by the video game "Portal").

public class Portal {
	
	private float volume = 0.35F;
	private Transform destination;
	
	public bool isOrange;
	public GameObject particles;
	public bool closeOnPass = false;
	public bool closeOnExit = false;
	public AudioClip Sound;
	
	void Start(){
	
	if (isOrange == false) {
		destination = GameObject.FindGameObjectWithTag("OrangePortal").GetComponent<Transform>();
		} else {
		destination = GameObject.FindGameObjectWithTag("BluePortal").GetComponent<Transform>();
		}
	}
	
	void OnTriggerEnter2D(Collider2D other){
	if (closeOnPass == true) {
			Destroy(GameObject.FindGameObjectWithTag("BluePortal"));
			ParticleEffect();
		}
		
	
	
	if (Vector2.Distance(transform.position, other.transform.position) > 0.3f) {
		
		 AudioSource.PlayClipAtPoint(Sound, transform.position , volume);
		 other.transform.position = new Vector2(destination.position.x, destination.position.y);
		}
	}
	
	void OnTriggerExit2D(Collider2D other){
		if (closeOnExit == true) {
			Destroy(GameObject.FindGameObjectWithTag("OrangePortal"));
			ParticleEffect();
		}
	}
	
	void ParticleEffect() {
		GameObject smokePuff = Instantiate (particles, transform.position, Quaternion.identity) as GameObject;
		smokePuff.particleSystem.startColor = gameObject.GetComponent<SpriteRenderer>().color;
	}
}
