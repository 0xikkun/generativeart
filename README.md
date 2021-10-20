float tree_angle;
float tree_length;
float tree_startx;
float tree_scale;
int tree_step;

 
void setup() {
    size(800, 450);
    tree_step = 7;
    tree_angle = 25;
    tree_length = 100;
    tree_scale = 0.7;
    tree_startx = width/2;
    tree_angle = radians(tree_angle);
    newTree();
}
 
void draw() {
    background(255);
    newTree();
    noLoop();
    saveFrame("screen-####.jpg");
}
 
void keyPressed() {
    if ( key == ' ' ) {
        save("tree.jpg");
  }
}
 
void newTree() {
    translate(tree_startx, height);
    branch(tree_length, tree_step);
}
 


void branch(float h, int n) {
    float theta;
    float i,j;

    colorMode( HSB, 360, 100, 100 ); 
    fill( 360/(tree_step + 1) * (tree_step - n), 100, 100 );
    strokeWeight(3);
    rect(0, -h, h, h);
    
    if (n > 0) {
        theta = -tree_angle;
        j = h * cos(tree_angle);
        pushMatrix();
        translate(0, -h);
        rotate(theta);        
        branch(j, n-1);
        popMatrix();
        
        theta = -PI/2 - tree_angle;
        i = h * sin(tree_angle);
        pushMatrix();
        translate(h, -h);
        rotate(theta);
        translate(i, 0);
        branch(-i, n-1);
        popMatrix(); 

    }




}
