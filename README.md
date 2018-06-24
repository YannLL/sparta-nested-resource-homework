# Sparta Weekend Homework - Rails nested routes

This backend project is mock database within a database, simulating books and authors. This is a bare-bones data management production and I used Ruby on Rails to accomplish it.

## Core task requirements

* Create a minimum of two resources
* One-to-many relationship
* Using an MVC model
* 7 RESTFUL routes for both resources 
 
## Operation Instructions

Fork/clone this repo via Github:
[git@github.com:YannLL/sparta-nested-resource-homework.git](git@github.com:YannLL/sparta-nested-resource-homework.git)

## Sample code
### 7 REST routes

~~~ ruby
# GET /books
  # GET /books.json
  def index
    @books = Book.all
  end

  # GET /books/1
  # GET /books/1.json
  def show
  end

  # GET /books/new
  def new
    @author = Author.find(params[:author_id])
    @book = Book.new
  end

  # GET /books/1/edit
  def edit
    @author = Author.find(params[:author_id])
  end

  # POST /books
  # POST /books.json
  def create
    @author = Author.find(params[:author_id])
    @book = Book.new(book_params)

    respond_to do |format|
      if @book.save
        format.html { redirect_to author_path(@author), notice: 'Book was successfully created.' }
        format.json { render :show, status: :created, location: @book }
      else
        format.html { render :new }
        format.json { render json: @book.errors, status: :unprocessable_entity }
      end
    end
  end

  # PATCH/PUT /books/1
  # PATCH/PUT /books/1.json
  def update
    respond_to do |format|
      if @book.update(book_params)
        format.html { redirect_to author_book_path, notice: 'Book was successfully updated.' }
        format.json { render :show, status: :ok, location: @book }
      else
        format.html { render :edit }
        format.json { render json: @book.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /books/1
  # DELETE /books/1.json
  def destroy
    @author = Author.find(params[:author_id])
    @book.destroy
    respond_to do |format|
      format.html { redirect_to author_path(@author), notice: 'Book was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  private
    # Use callbacks to share common setup or constraints between actions.
    def set_book
      @book = Book.find(params[:id])
    end

    # Never trust parameters from the scary internet, only allow the white list through.
    def book_params
      params.require(:book).permit(:title, :genre, :published, :author_id)
    end
end
~~~