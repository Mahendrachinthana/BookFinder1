// BookFinderApp.js
import React, { useState } from "react";

const BookFinderApp = () => {
  const [searchTerm, setSearchTerm] = useState("");
  const [books, setBooks] = useState([]);
  const [loading, setLoading] = useState(false);

  // Function to fetch books based on the search term
  const fetchBooks = async () => {
    if (searchTerm.trim() === "") return;
    setLoading(true);

    try {
      const response = await fetch(
        `https://openlibrary.org/search.json?title=${searchTerm}`
      );
      const data = await response.json();
      setBooks(data.docs.slice(0, 10)); // Limiting to the top 10 results
    } catch (error) {
      console.error("Error fetching books:", error);
    } finally {
      setLoading(false);
    }
  };

  // Function to handle form submission
  const handleSearch = (e) => {
    e.preventDefault();
    fetchBooks();
  };

  return (
    <div style={styles.app}>
      <h1 style={styles.title}>Book Finder for Alex</h1>
      <form onSubmit={handleSearch} style={styles.searchForm}>
        <input
          type="text"
          placeholder="Search by book title"
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
          style={styles.searchInput}
        />
        <button type="submit" style={styles.searchButton}>
          Search
        </button>
      </form>

      {loading && <p style={styles.loadingText}>Loading...</p>}

      <div style={styles.bookList}>
        {books.map((book, index) => (
          <div key={index} style={styles.bookCard}>
            <h3 style={styles.bookTitle}>{book.title}</h3>
            <p style={styles.bookAuthor}>
              <strong>Author:</strong>{" "}
              {book.author_name?.join(", ") || "Unknown"}
            </p>
            {book.cover_i ? (
              <img
                src={`https://covers.openlibrary.org/b/id/${book.cover_i}-M.jpg`}
                alt={`${book.title} cover`}
                style={styles.bookCover}
              />
            ) : (
              <div style={styles.noCover}>No Cover Available</div>
            )}
          </div>
        ))}
      </div>
    </div>
  );
};

// Inline CSS styles
const styles = {
  app: {
    textAlign: "center",
    fontFamily: "Arial, sans-serif",
    minHeight: "100vh",
    padding: "2rem",
    background: "linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%)",
    color: "#333",
  },
  title: {
    fontSize: "2.5rem",
    fontWeight: "bold",
    color: "#fff",
    marginBottom: "1.5rem",
  },
  searchForm: {
    marginBottom: "2rem",
    display: "flex",
    justifyContent: "center",
    flexWrap: "wrap",
  },
  searchInput: {
    padding: "0.75rem",
    fontSize: "1rem",
    borderRadius: "8px 0 0 8px",
    border: "1px solid #ddd",
    outline: "none",
    width: "300px",
    maxWidth: "80vw",
  },
  searchButton: {
    padding: "0.75rem 1.5rem",
    fontSize: "1rem",
    borderRadius: "0 8px 8px 0",
    border: "none",
    backgroundColor: "#ff6b6b",
    color: "#fff",
    cursor: "pointer",
    transition: "background-color 0.3s ease",
  },
  loadingText: {
    color: "#fff",
    fontSize: "1.2rem",
  },
  bookList: {
    display: "flex",
    flexWrap: "wrap",
    gap: "1.5rem",
    justifyContent: "center",
  },
  bookCard: {
    width: "220px",
    padding: "1.5rem",
    borderRadius: "10px",
    backgroundColor: "#fff",
    boxShadow: "0px 4px 12px rgba(0, 0, 0, 0.1)",
    transition: "transform 0.3s ease",
  },
  bookTitle: {
    fontSize: "1.2rem",
    fontWeight: "bold",
    color: "#333",
    marginBottom: "0.5rem",
  },
  bookAuthor: {
    color: "#777",
    fontSize: "0.9rem",
    marginBottom: "1rem",
  },
  bookCover: {
    width: "100%",
    height: "auto",
    borderRadius: "8px",
    marginTop: "1rem",
  },
  noCover: {
    fontSize: "0.9rem",
    color: "#666",
    marginTop: "1rem",
  },

  // Responsive styling using media queries
  "@media (max-width: 768px)": {
    title: {
      fontSize: "2rem",
    },
    searchInput: {
      width: "250px",
      fontSize: "0.9rem",
    },
    searchButton: {
      padding: "0.5rem 1rem",
      fontSize: "0.9rem",
    },
    bookCard: {
      width: "180px",
      padding: "1rem",
    },
    bookTitle: {
      fontSize: "1rem",
    },
  },

  "@media (max-width: 480px)": {
    title: {
      fontSize: "1.8rem",
    },
    searchInput: {
      width: "200px",
      fontSize: "0.8rem",
    },
    searchButton: {
      padding: "0.5rem 0.8rem",
      fontSize: "0.8rem",
    },
    bookList: {
      flexDirection: "column",
      gap: "1rem",
    },
    bookCard: {
      width: "90%",
    },
  },
};

export default BookFinderApp;
